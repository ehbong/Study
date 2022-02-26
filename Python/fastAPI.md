# FastAPI
* [FastAPI 공식문서](https://fastapi.tiangolo.com/ko/)
* [FastAPI 공식 풀스택 구성](https://github.com/tiangolo/full-stack-fastapi-postgresql/tree/master/%7B%7Bcookiecutter.project_slug%7D%7D/backend/app/app)

* [FastAPI sqlalchemy 연결 설정](https://dingrr.com/blog/post/python-fastapi-%EB%A1%9C-%EB%B0%B1%EC%97%94%EB%93%9C-%EB%A7%8C%EB%93%A4%EA%B8%B0-3%ED%99%94-mysql-%EC%97%B0%EA%B2%B0)
* [FastAPI 유튜브 기본강의](https://www.youtube.com/watch?v=7frN5JPMsQU&list=PLr_ki3_GfpZMTSdQehJRrIwuDGOHh5LvB&index=7)
* [FastAPI 다른 강의](https://www.youtube.com/watch?v=ktGVFmfGiGM&list=PLKy1qiqTzJteucwpykHuZyCh-HqeZXIG4&index=17)
* [FastAPI Websocket](https://fastapi.tiangolo.com/ko/advanced/websockets/?h=web)
* [FastAPI 블로그](https://lucky516.tistory.com/86?category=1060055)
* [uvloop 설명](https://koreapy.tistory.com/1124)
* [FastAPI Event 다루기](https://www.hides.kr/1091?category=666044)

* [swagger 주석](https://fastapi.tiangolo.com/tutorial/metadata/)
```python
   # swagger 주석 
   @app.post("/test")
   def endpoint():
    """
     들여쓰기 하면 박스처리
     ***별처리 하면 굵은 글씨***
     <b>HTML테그도 적용</b>
    """
    print('/test')
    return {}
   
```


>  swagger 쓸때 토큰 인증이 필요한 API 호출 시\
>  swagger 에 토큰 헤더 기능 추가
```python
 import fastapi import APIKeyHeader
 
 API_KEY_HEADER = APIKeyHeader(name="Authorization", auto_error=False)
 
 app.include_router(test.router, dependencise=[Depends(API_KEY_HEADER)])
```

### pydantic 

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
      
# 폼 모델 정의  
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
```

* [모델 컬럼 길이 정의](https://stackoverflow.com/questions/61326020/how-can-i-set-max-string-field-length-constraint-in-pydantic)
```python
from pydantic import BaseModel, constr

class MyPydanticModel(BaseModel):
    name: constr(max_length=10)
```
