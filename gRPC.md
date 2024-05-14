### gRPC
* [gRPC 공식문서](https://grpc.io/)
* [python gRPc](https://grpc.io/docs/languages/python/quickstart/)
* [python gRpc 예제실행](https://hororolol.tistory.com/188)
* [mac 에서 발생한 Descriptors cannot not be created directly 오류 대처](https://stackoverflow.com/questions/72441758/typeerror-descriptors-cannot-not-be-created-directly)
* [Golang gRPC server 구축하기](https://devjin-blog.com/golang-grpc-server-1/)
* [뱅크샐러드 grpc 적용기](https://blog.banksalad.com/tech/production-ready-grpc-in-golang/)
* [gRPC GIT](https://github.com/grpc)
* [gRPC vs http api 비교](https://docs.microsoft.com/ko-kr/aspnet/core/grpc/comparison?view=aspnetcore-6.0)
* [gRPC 특징 및 간단 설명](https://youtu.be/uwrR5e5_FH8?si=-6AuApaXTjHHtG0k)
  
|특징|설명|
|----|----|
|protocal Buffer 기반 직렬화|이진 직렬화를 제공해서 데이터 교환이 빠름|
|Cross-Language|다양한 프로그래밍 언어 지원|
|HTTP/2 기반|헤더압축, 다중화, 이진데이터 전송 등 지원|
|양방향 스트리밍|양방향 스트림 전송|
|보안|SSL/TLS 통신 암호화|


#### proto 파일 작성
> syntax: 문법 및 grpc 버전 지정([proto3 버전 작성 공식문서](https://protobuf.dev/programming-guides/proto3/))
```proto
syntax = "proto3";
```
> message: 주고 받는 데이터의 형태 및 구조 정의
```proto
message MyMessage { 
	string name = 1; 
	int32 age = 2; 
}
```
> service: gpc를 통해 상호작용하기 위한 메소드 정의
```proto
service MyService { 
	rpc 메서드명 (param message) returns (return message);
	rpc GetData (MyRequest) returns (MyResponse); 
}
```

> proto 파일 컴파일 명령어<br>
> `grpc_tools.protoc` grpc_tools 패키지의 protoc 유틸리티를 사용하여 chat.proto 파일을 컴파일하는 명령어<br>
> `-I.` include 디렉토리를 현재 디렉토리로 설정<br>
> `--python_out=.` 파이썬 파일들의 출력을 현재 디렉토리로 설정<br>
> `--grpc_python_out=.` gRPC 파이썬 코드 파일의 출력을 현재 디렉토리로 설정
> `chat.proto` proto 파일명
```bash
$ python -m grpc_tools.protoc -I. --python_out=. --grpc_python_out=. chat.proto
```

> 기본적인 요청, 응답 예제 코드
```python
 # 서버 예제 코드 및 설명
 from concurrent import futures
 import grpc
 import example_pb2
 import example_pb2_grpc

 class ExampleService(example_pb2_grpc.ExampleServiceServicer):
     # ExampleServiceServicer 클래스를 상속하며 SayHello 메서드를 구현합니다.
     def SayHello(self, request, context):
         # 클라이언트로부터 받은 name 값을 사용하여 응답 메시지를 만듭니다.
         return example_pb2.HelloResponse(message="Hello, {}!".format(request.name))

 # gRPC 서버 인스턴스를 만듭니다.
 server = grpc.server(futures.ThreadPoolExecutor(max_workers=10))

 # 서버에 ExampleServiceServicer 인스턴스를 추가합니다.
 example_pb2_grpc.add_ExampleServiceServicer_to_server(ExampleService(), server)

 # 서버를 50051 포트로 시작합니다.
 # [::] 은 IPv6의 모든 주소를 나타내는 표현법으로 IPv4에서는 0.0.0.0 으로 사용되는데,
 # 해당 표기 법을 사용하번 IPv4와 IPv6 모두에서 클라이언트 요청을 처리 할 수 있다.
 server.add_insecure_port('[::]:50051')
 server.start()

 print("Server started. Listening on port 50051.")
 # 서버가 종료될 때까지 대기합니다. 
 # grpc 서버는 다수의 클라이언트 연결 요청을 처리하기 위해 계속 실행되어야 합니다. 
 # 따라서 wait_for_termination()을 호출하여 서버가 종료될 때까지 실행을 유지하며 클라이언트 연결 요청을 수신할 수 있도록 합니다.
 # 서버를 종료하려면 다른 스레드에서 server.stop() 메소드를 호출하여 서버를 중지
 server.wait_for_termination()
```
```python
 # 클라이언트 예제 코드 및 설명
 import grpc
 import example_pb2
 import example_pb2_grpc

 def run():
     # 'SERVER_IP_ADDRESS'에 서버의 IP 주소를 입력하여 채널을 생성합니다.
     # 만약 서버가 구동 중이 아니거나 주소가 틀릴 경우 grpc.RpcError 예외 발생
     with grpc.insecure_channel('SERVER_IP_ADDRESS:50051') as channel:
         # 채널을 사용하여 Stub 인스턴스를 생성합니다.
         stub = example_pb2_grpc.ExampleServiceStub(channel)
         # 서버에 SayHello 메서드를 호출하고, 반환된 응답을 받습니다.
         response = stub.SayHello(example_pb2.HelloRequest(name="John"))
     print("Response received: " + response.message)

 if __name__ == '__main__':
     run()

```

> 양방향 통신 예제 코드
```python
 # 양방향 통신 서버코드(연결 유지 특성)
 import grpc
 from concurrent import futures
 import time

 # pb 파일에서 생성된 모듈을 import 합니다.
 import chat_pb2
 import chat_pb2_grpc

 class ChatServicer(chat_pb2_grpc.ChatServicer):
     # 클라이언트가 서버로 메시지를 전송할 때 호출됩니다.
     def Chat(self, request_iterator, context):
         # 클라이언트로부터 받은 메시지를 출력합니다.
         for request in request_iterator:
             print("Client message received: " + request.message)

             # 클라이언트에게 메시지를 응답으로 전송합니다.
             yield chat_pb2.Message(message="Server received message: " + request.message)

 def serve():
     # gRPC 서버를 생성합니다.
     server = grpc.server(futures.ThreadPoolExecutor(max_workers=10))

     # 서비스를 gRPC 서버에 추가합니다.
     chat_pb2_grpc.add_ChatServicer_to_server(ChatServicer(), server)

     # 서버를 시작합니다.
     server.add_insecure_port("[::]:50051")
     server.start()
     print("Server started. Listening on port 50051...")

     # 서버가 종료되지 않도록 유지합니다.
     try:
         while True:
             time.sleep(86400)
     except KeyboardInterrupt:
         server.stop(0)

```
```python
 # 양방향 통신 클라이언트코드(연결 유지 특성)
 import grpc

 # pb 파일에서 생성된 모듈을 import 합니다.
 import chat_pb2
 import chat_pb2_grpc

 def run():
     # 서버에 연결할 gRPC 채널을 생성합니다.
     channel = grpc.insecure_channel("localhost:50051")

     # 채팅 서비스 스텁을 생성합니다.
     stub = chat_pb2_grpc.ChatStub(channel)

     # 서버에 전송할 메시지를 입력받습니다.
     while True:
         message = input("Enter your message: ")

         # 서버에 메시지를 전송합니다.
         response = stub.Chat(iter([chat_pb2.Message(message=message)]))

         # 서버로부터 받은 응답을 출력합니다.
         for res in response:
             print("Server message received: " + res.message)

 if __name__ == "__main__":
     run()

```
