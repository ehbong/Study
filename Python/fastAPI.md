# FastAPI
* [FastAPI 공식문서](https://fastapi.tiangolo.com/ko/)
* [FastAPI 공식 풀스택 구성 vue, postgresql](https://github.com/tiangolo/full-stack-fastapi-postgresql/tree/master/%7B%7Bcookiecutter.project_slug%7D%7D/backend/app/app)

* [FastAPI sqlalchemy 연결 설정](https://dingrr.com/blog/post/python-fastapi-%EB%A1%9C-%EB%B0%B1%EC%97%94%EB%93%9C-%EB%A7%8C%EB%93%A4%EA%B8%B0-3%ED%99%94-mysql-%EC%97%B0%EA%B2%B0)
* [FastAPI 유튜브 기본강의](https://www.youtube.com/watch?v=7frN5JPMsQU&list=PLr_ki3_GfpZMTSdQehJRrIwuDGOHh5LvB&index=7)
* [FastAPI 다른 강의](https://www.youtube.com/watch?v=ktGVFmfGiGM&list=PLKy1qiqTzJteucwpykHuZyCh-HqeZXIG4&index=17)

* [FastAPI 시작, 종료 이벤트](https://fastapi.tiangolo.com/advanced/events/)
* [공식문서 CORS설정](https://fastapi.tiangolo.com/ko/tutorial/cors/)
* [CORS 설정](https://developer-itspjc.tistory.com/m/25)
* [FastAPI 블로그](https://lucky516.tistory.com/86?category=1060055)

* [FastAPI의 경로 설정은 순차적용](https://fastapi.tiangolo.com/ko/tutorial/path-params/#_7)
```python 
from fastapi import FastAPI

app = FastAPI()

## /users/me 보다 /users/{user_id}를 먼저 선언하면, me 가 user_id로 인식

@app.get("/users/me")
async def read_user_me():
    return {"user_id": "the current user"}


@app.get("/users/{user_id}")
async def read_user(user_id: str):
    return {"user_id": user_id}
```
* [uvloop 설명](https://koreapy.tistory.com/1124)

* [FastAPI Event 다루기](https://www.hides.kr/1091?category=666044)
* [request File](https://fastapi.tiangolo.com/tutorial/request-files/)

* [error 처리](https://lucky516.tistory.com/101)

* [tag 활용](https://fastapi.tiangolo.com/tutorial/metadata/)
* [swagger 페이지 접근 권한 로그인 설정](https://fastapi.tiangolo.com/advanced/security/http-basic-auth/)

***
* [FastAPI BackgroundTasks](https://fastapi.tiangolo.com/tutorial/background-tasks/)
> 오래걸리는 작업은 우선 응답을 해주고 백그라운드에서 작업을 BackgroundTasks 로 처리

***
* [swagger 주석](https://fastapi.tiangolo.com/tutorial/metadata/)
```python
   # swagger 주석 
   @app.post("/test")
   def endpoint():
    """
     들여쓰기 + \n 하면 박스처리 그 다음 줄부터 적용 
     ***별처리 하면 굵은 글씨***
     <b>HTML테그도 적용</b>
    """
    print('/test')
    return {}
   
```
```python
from fastapi import FastAPI

app = FastAPI()

# 스웨거에서 엔드포인트 제외 설정 include_in_schema=False
@app.get("/items/", include_in_schema=False)
async def read_items():
    return [{"item_id": "Foo"}]

```
>  swagger 쓸때 토큰 인증이 필요한 API 호출 시\
>  swagger 에 토큰 헤더 기능 추가
```python
 import fastapi import APIKeyHeader
 
 API_KEY_HEADER = APIKeyHeader(name="Authorization", auto_error=False)
 
 app.include_router(test.router, dependencise=[Depends(API_KEY_HEADER)])
```
```python
   # 스웨거에 호출 지연 시간 표시 옵션
   app = FastAPI(swagger_ui_parameters={"displayRequestDuration": True})
```

### pydantic 

> Response 할때 JSONResponse 등으로 감싸면 모델 처리가 안됨.
* [JSONResponse 사용에 대한 공식문서](https://fastapi.tiangolo.com/advanced/response-directly/)

* [form 데이터 처리 방법](https://github.com/tiangolo/fastapi/issues/2387)
```python
# pydantic model
# 데코레이션 함수 작성
def as_form(cls: Type[BaseModel]):
  """
  Adds an as_form class method to decorated models. The as_form class method
  can be used with FastAPI endpoints
  """
  new_params = [
      inspect.Parameter(
          field.alias,
          inspect.Parameter.POSITIONAL_ONLY,
          default=(Form(field.default) if not field.required else Form(...)),
          annotation=field.outer_type_,
      )
      for field in cls.__fields__.values()
  ]

  async def _as_form(**data):
      return cls(**data)

  sig = inspect.signature(_as_form)
  sig = sig.replace(parameters=new_params)
  _as_form.__signature__ = sig
  setattr(cls, "as_form", _as_form)
  return cls
      
# 폼 모델 정의 (단한개의 값이라도 바디에서 받으려면 모델 생성 필요) 
@as_form
class Item(BaseModel):
    name: str
    another: str
    opts: Dict[str, int] = {}
    

# 폼 모델 사용 법 + 파일 데이터 수신 방법
@app.post("/test", response_model=Item)
def endpoint(item: Item = Depends(Item.as_form), data: bytes = File(...)):
    print(len(data))
    return item

# 필수값이 아닌 값 설정 Optional
from typing import Optional

class Item(BaseModel):
    name: Optional[str]
    another: str
    opts: Dict[str, int] = {}
    
# 정해진 값만 받는 경우 enum
class ItemType(str, Enum):
   box: str = "B"
   roll: str = "R"
    
# 모델 객체를 dict로 변환
@app.post("/test", response_model=Item)
def endpoint(item: Item):
    # dict 변환 방법1 내부에 모델객체가 또 있을경우 변환되지 않음
    dict(item)
    # dict 변환 방법2 내부에 모델객체도 전부 변환 됨
    item.dict()
    return item

# 요청에서 필수값이 아닌 요청을 할때는 = None을 넣음
@app.post("/test", response_model=Item)
def endpoint(param : str = None ):
   print(param)
   return None

```

> post에 모델로 바디 데이터를 받을 때 값이 필수가 아니더라도 바디가 없으면 오류 발생

* [모델 컬럼 길이 정의](https://stackoverflow.com/questions/61326020/how-can-i-set-max-string-field-length-constraint-in-pydantic)
```python
from pydantic import BaseModel, constr

class MyPydanticModel(BaseModel):
    name: constr(max_length=10)
```

> 웹소켓
* [FastAPI Websocket](https://fastapi.tiangolo.com/ko/advanced/websockets/?h=web)
* [FastAPI Websocket 채팅방 생성](https://sdamoosavi.medium.com/chatroom-development-with-fastapi-websocket-1c96880412d7)
* [FastAPI Websocket 토큰 추가](https://indominusbyte.github.io/fastapi-jwt-auth/advanced-usage/websocket/)
* [FastAPI Websocket Db Broadcaster](https://github.com/encode/broadcaster)
```python
   # connect 시 while 로 종료되지 않게 붙잡고 있어야 유지
```
