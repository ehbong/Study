# AWS Lambda 는 함수를 저장했다가 특정한 시점, 이벤트에 반응해 실행하는 서비스
# Lambda 통해 서버가 없는 API 서버를 만들 수 있다.


* [생활코딩 AWS Lambda에 대한 강의](https://youtu.be/t8sjTFM_tfE)

* [Lambda API 설정방법 및 절차](https://medium.com/@yumenohosi/aws-lambda-api-gateway-dynamodb-node-js-%EC%82%AC%EC%9A%A9%EA%B8%B0-%EC%82%BD%EC%A7%88%EA%B8%B0-b5352e00b396)

* [Lambda 에 대한 개발 절차](https://daddyprogrammer.org/post/9131/aws-lambda-setup-develop-environment/)

* [Lambda Rest API 만들기](https://blog.msalt.net/222)

* [AWS Architecting Serverless Solutions 강의](https://www.aws.training/Details/eLearning?id=70986)

* [서버리스 대용량 트래픽처리 예제](https://catalog.us-east-1.prod.workshops.aws/workshops/05e3e1f9-5d5a-4cc5-9899-df114def68e7/ko-KR/lab1)

* [Lambda rds 연결](https://dev.classmethod.jp/articles/lambda-rds-interlock/)

* [Lambda vs ec2 비용 비교](https://dev.classmethod.jp/articles/amazon-ec2-vs-aws-lambda-price/)


### 요청을 받아서 DB에 저장하는 예제

```python
import json
import pymysql

# RDS 연결 정보
rds_host = "your_rds_host"
name = "your_rds_username"
password = "your_rds_password"
db_name = "your_rds_db_name"

# RDS 연결 함수
def connect():
    try:
        conn = pymysql.connect(rds_host, user=name, passwd=password, db=db_name, connect_timeout=5)
    except pymysql.MySQLError as e:
        print("ERROR: Could not connect to MySQL instance.")
        print(e)
        raise e
    
    return conn

def lambda_handler(event, context):
    # POST 요청에서 데이터 추출
    data = json.loads(event['body'])
    name = data['name']
    age = data['age']
    
    # RDS에 데이터 저장
    conn = connect()
    with conn.cursor() as cur:
        cur.execute("INSERT INTO my_table (name, age) VALUES (%s, %s)", (name, age))
    conn.commit()
    conn.close()
    
    # 응답 생성
    response_data = {'message': 'Data saved successfully'}
    response = {
        'statusCode': 200,
        'headers': {
            'Content-Type': 'application/json'
        },
        'body': json.dumps(response_data)
    }
    
    return response
    
```
1. AWS Lambda 콘솔로 이동합니다.
2. "함수 만들기" 버튼을 클릭합니다.
3. "서버리스 앱 및 API" 항목에서 "함수"를 선택합니다.
4. "새로운 함수 만들기" 버튼을 클릭합니다.
5. 함수 이름, 런타임, 역할 등 필요한 정보를 입력합니다.
6. "함수 생성" 버튼을 클릭합니다.
7. 함수 코드를 "코드 입력 유형"에서 "직접 입력"으로 변경합니다.
8. 위 코드를 붙여넣습니다.
9. "배포" 버튼을 클릭


### 함수 URL 에 연결
1. AWS Management Console에서 API Gateway 서비스를 선택합니다.
2. "REST API 생성" 버튼을 클릭합니다.
3. "REST API"를 선택하고 "빈 API"를 선택한 후, "API 만들기" 버튼을 클릭합니다.
4. "작업" 메뉴에서 "리소스 만들기"를 선택합니다.
5. 리소스 이름을 입력하고 "만들기" 버튼을 클릭합니다.
6. 만든 리소스에서 "작업" 메뉴에서 "메서드 생성"을 선택합니다.
7. 메서드를 선택하고 "Lambda 함수"를 선택한 후, Lambda 함수 이름을 입력합니다.
8. "작업" 메뉴에서 "메서드 요청"을 선택합니다.
9. "HTTP 요청 본문"에서 "템플릿 추가"를 선택하고, "application/json"을 선택한 후, 다음과 같은 템플릿을 입력합니다.
```javascript
#set($inputRoot = $input.path('$'))
{
"body": $input.json('$')
}
```
10. "작업" 메뉴에서 "메서드 응답"을 선택합니다.
11. "HTTP 응답 본문"에서 "application/json"을 선택하고, 응답 JSON 형식을 입력합니다.
12. "작업" 메뉴에서 "배포"를 선택합니다.
13. "새로운 스테이지"를 선택하고, 스테이지 이름을 입력한 후, "배포" 버튼을 클릭합니다.
14. 생성된 API Gateway URL을 확인합니다.


### Layer
> * 라이브러리 레이어 생성(python)
> 	1. 필요한 라이브러리 다운로드: 로컬 콘솔창에 아래 명령어로 현재 폴더에 다운로드	
```bash
pip install <라이브러리> -t . 
```
> 	2. 해당 라이브러리 들을 python(소문자로) 이라는 폴더 생성 후 넣음
> 	3. python을 감싸는 폴더를 임의의 이름으로 생성해서 넣고 해당 폴더 압축
> 	4. lambda 의 layer(계층) 메뉴에서 생성 후 파일 업로드
> 	5. lambda 함수에 layer 연결


##### CORS 설정
* API Gateway 의 리소스 메뉴에서 설정
* Lambda 함수의 리턴 헤더에 설정 추가 : Access-Control-Allow-Origin


