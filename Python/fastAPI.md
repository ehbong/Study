# FastAPI
* [FastAPI 공식문서](https://fastapi.tiangolo.com/ko/)
* [FastAPI 공식 풀스택 구성](https://github.com/tiangolo/full-stack-fastapi-postgresql/tree/master/%7B%7Bcookiecutter.project_slug%7D%7D/backend/app/app)

* [FastAPI sqlalchemy 연결 설정](https://dingrr.com/blog/post/python-fastapi-%EB%A1%9C-%EB%B0%B1%EC%97%94%EB%93%9C-%EB%A7%8C%EB%93%A4%EA%B8%B0-3%ED%99%94-mysql-%EC%97%B0%EA%B2%B0)
* [FastAPI 유튜브 기본강의](https://www.youtube.com/watch?v=7frN5JPMsQU&list=PLr_ki3_GfpZMTSdQehJRrIwuDGOHh5LvB&index=7)
* [FastAPI 다른 강의](https://www.youtube.com/watch?v=ktGVFmfGiGM&list=PLKy1qiqTzJteucwpykHuZyCh-HqeZXIG4&index=17)
* [FastAPI Websocket](https://fastapi.tiangolo.com/ko/advanced/websockets/?h=web)
* [FastAPI 블로그](https://lucky516.tistory.com/86?category=1060055)
* [uvloop 설명](https://koreapy.tistory.com/1124)

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
```
