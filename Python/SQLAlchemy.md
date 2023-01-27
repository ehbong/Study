# SQLAlchemy

## 파이썬 ORM 모듈
### 다른 ORM
* [tortoise-orm](https://tortoise-orm.readthedocs.io/en/latest/)
### 설치방법

```bash
  pip3 install sqlalchemy
```


* [SQLAlchemy 공식사이트](https://www.sqlalchemy.org/)

* [SQLAlchemy 튜토리얼](https://riptutorial.com/ko/sqlalchemy)

* [SQLAlchemy 튜토리얼 번역1](https://edykim.com/ko/post/getting-started-with-sqlalchemy-part-1/)

* [SQLAlchemy 튜토리얼 번역2](https://edykim.com/ko/post/getting-started-with-sqlalchemy-part-2/)

* [flask_sqlalchemy](https://opentutorials.org/module/3669/22070)

* [SQLAlchemy SQL 호출예제](https://lowelllll.github.io/til/2019/04/19/TIL-flask-sqlalchemy-orm/)

* [SqlAlchemy 모델로 DB테이블 생성](https://gggggeun.tistory.com/77)

* [SqlAlchemy geohash 값으로 주변 검색](https://github.com/Jd007/adaptive-geohash-sql)

* [이미 있는 DB의 모델정보 가져오기 for flask](https://beomi.github.io/2017/10/20/DB-To-SQLAlchemy-Model/)
```bash
  # 디비 모델 정보 가져오기
  pip install flask-sqlacodegen
  flask-sqlacodegen "mysql://username:password@DB_IP/DB_NAME" --flask > models.py
  
  # db커넥션 연결을 유지하려면 DB설정의 time_out 시간보다 pool_recycle 설정 값이 작아야함.
```
* [이미 있는 DB의 모델정보 가져오기](https://wooiljeong.github.io/python/sqlacodegen/)
```bash
   # 스키마 등 옵션 가능
   sqlacodegen --schema=myschema --tables=mytable '<디비타입>://myuser:mypassword@myhost:port/database' > model.py
```

```python
  from sqlalchemy import create_engine
  
  # 연결하면서 기본 타임존 설정하기 connect_args=={'options': '-c timezone=Asia/Seoul'}
  engine = create_engine("postgresql://user:password@host:port/dbname", 
                          connect_args={'options': '-c timezone=Asia/Seoul'})
```

* [func 함수에 대해](https://item4.blog/2015-07-05/Internal-of-sqlalchemy.sql.expression.func/)

* [동적쿼리1](https://stackoverflow.com/questions/37336520/sqlalchemy-dynamic-filter)

* [동적쿼리2 2022.08.08 접속안됨](https://stackoverrun.com/ko/q/10784033)

* [nvl 역할을 하는 func.coalesce](https://programtalk.com/python-examples/sqlalchemy.sql.func.coalesce/)

* [in 조건](https://stackoverflow.com/questions/8603088/sqlalchemy-in-clause)

* [특정 컬럼만 출력](https://qastack.kr/programming/11530196/flask-sqlalchemy-query-specify-column-names)

* [테이블 별칭 & 조인](https://edykim.com/ko/post/getting-started-with-sqlalchemy-part-2/)

* [Hybrid Attributes 공식문서](https://docs.sqlalchemy.org/en/13/orm/extensions/hybrid.html) 

* [Hybrid Attributes를 이용한 암호화](https://spoqa.github.io/2011/12/10/sqlalchemy-hybrid-attributes.html)

* [여러 DB를 사용중일때 특정 연결(엔진)을 불러올때](https://github.com/pallets/flask-sqlalchemy/issues/359)

* [insert or update](https://stackoverflow.com/questions/7165998/how-to-do-an-upsert-with-sqlalchemy)

* [SQLAlchemy + Graphene로 GraphQL 구현](https://blog.neonkid.xyz/254?category=656103)

* [한 테이블의 여러 관계키 연결 할때 오류 해결 방법](https://stackoverflow.com/questions/44434410/sqlalchemy-multiple-foreign-key-pointing-to-same-table-same-attribute)

> 관계를 이용한 insert 시 add 와 상관없이 부모가 commit 될때 데이터가 반영.<br>
session.add 로 들어갈 데이터와 들어가지 않을 데이터를 구분할 수 없음<br>
session.expunge(obj) 로 가능하지만 관계가 설정될 경우 컨트롤이 어려움<br>
[관계 insert시 add 반영에 대한 질답](https://stackoverflow.com/questions/71456425/i-was-wondering-how-to-prevent-objects-not-added-to-sqlalchemy-from-being-commit)

* [SQLAlchemy의 연결 풀링 이해하기](https://spoqa.github.io/2018/01/17/connection-pool-of-sqlalchemy.html)

* [비동기 처리](https://ellune.tistory.com/73)

* [SQLAlchemy 세션 관리](https://planbs.tistory.com/entry/Engine%EA%B3%BC-Session-Scoped-Session)

* [SQLAlchemy bulk insert](https://velog.io/@samnaka/sqlalchemy-bulk-insert)

* [SQLAlchemy model 관계를 이용해서 flush 사용없이 insert](https://stackoverflow.com/questions/71285679/how-to-speed-up-python-and-sqlalchemy)

* [sqlalchemy data convert dict](https://stackoverflow.com/questions/1958219/how-to-convert-sqlalchemy-row-object-to-a-python-dict)

* [테이블데이터 객체를 dict로 변환](http://daplus.net/python-sqlalchemy-%ED%96%89-%EA%B0%9D%EC%B2%B4%EB%A5%BC-python-dict%EB%A1%9C-%EB%B3%80%ED%99%98/)
> pandas 없이 dict로 변환
```python
for u in session.query(<테이블>).all():
  print u.__dict__
```
```python
# sqlquery 데이터 또는 sqldata 를 dictlist 또는 list로 변환
def convert_sql_data_to_dict(list_or_query=[], data=None):
    if type(list_or_query) is BaseQuery or len(list_or_query) > 0:
        return [delete_sa_instance_state(row) for row in list_or_query]
    if data is not None:
        return delete_sa_instance_state(data)
    return None

# sa_instance_state 키 삭제
def delete_sa_instance_state(row):
    dict_data = row.__dict__
    del dict_data['_sa_instance_state']
    return dict_data
    
#### 다른방법
# 디비 모델 테이블에 소스 추가
from sqlalchemy.ext.declarative import as_declarative
from sqlalchemy import inspect


@as_declarative()
class Base:
    def _asdict(self):
        return {c.key: getattr(self, c.key)
                for c in inspect(self).mapper.column_attrs}
         
# 사용처에서
def convert_sql_data_to_dict(list_or_query=[], data=None):
    if type(list_or_query) is BaseQuery or len(list_or_query) > 0:
        return [row._asdict() for row in list_or_query]
    if data is not None:
        return data._asdict()
    return None
```
> 여러 DB를 사용중일때 특정 연결(엔진)을 불러올때
```python
##여러 DB를 사용중일때 특정 연결(엔진)을 불러올때
 db.get_engine(app, <bind명>)
 
## 그룹 바이
.group_by(<컬럼명>)

## sum
func.sum()

## count
func.count()

## distinct 컬럼값 중복 제거
from sqlalchemy import distinct
func.count(distinct(User.name))

## 두 쿼리의 결과값을 결합(유니온)
<a query>.union(<b query>)

## 날짜형식의 값을 문자열 형식으로 표현(mysql 기준)
func.date_format(<컬럼명>, '%Y-%m-%d')

## 날짜형식의 값을 문자열 형식으로 표현(postgresql 기준)
func.to_char(<컬럼명>, 'YYYY-MM-DD')

## 특정 컬럼 + 컬럼명을 조회할때
.with_entities(<테이블명>.<컬럼명>.label(<바꿀 컬럼명>), <테이블명>.<컬럼명>.label(<바꿀 컬럼명>), ...)
```


> SQLAlchemy 사용 시 멀티테스킹 + eventlet 을 사용하면 
> Commands out of sync; you can’t run this command now 에러가 발생할 수 있다. [링크](https://docs.sqlalchemy.org/en/13/faq/connections.html#commands-out-of-sync-you-can-t-run-this-command-now-this-result-object-does-not-return-rows-it-has-been-closed-automatically)
> 

### 암호화
* [SQLAlchemy-Utils 활용 컬럼 암호화](https://blog.linewalks.com/archives/7645)
```python
  import sqlalchemy as sa
  from sqlalchemy.orm import declarative_base
  from sqlalchemy_utils import EncryptedType
  ## AesEngine, AesGcmEngine
  ## 암호화 정도는 AesEngine(cbc) < AesGcmEngine(gcm)
  ## 해당 컬럼으로 조회를 하려면 AesEngine 을 사용
  ## secretkey가 틀릴 경우 오류 발생
  from sqlalchemy_utils.types.encrypted.encrypted_type import AesEngine

  Base = declarative_base()

  secretkey = "1234567812345678"
  
  class TableModel(Base):
    __tablename__ = "patient"
    id = sa.Column(sa.Integer, sa.Sequence("pid_seq"), primary_key=True)
    data = sa.Column(EncryptedType(sa.String, secretkey, AesEngine, "pkcs5"))
    
```


# Pandas
* [pandas](http://pythonstudy.xyz/python/article/408-pandas-%EB%8D%B0%EC%9D%B4%ED%83%80-%EB%B6%84%EC%84%9D)
* [pandas로 데이터 출력](https://lemontia.tistory.com/844)
* [pandas 의 to_sql 이용한 Bulk insert](https://tzara.tistory.com/119)
* [dataframe 활용](https://teddylee777.github.io/pandas/10minutes-to-pandas-%EB%B6%80%EB%8F%99%EC%82%B0%EC%8B%A4%EC%A0%9C%EB%8D%B0%EC%9D%B4%ED%84%B0-%ED%99%9C%EC%9A%A9%ED%95%98%EA%B8%B0)
* [dataframe 에서 값 검색](https://www.delftstack.com/ko/howto/python-pandas/pandas-get-index-of-row/)
* [DataFrame 조회, 정렬(sort), 조건필터(loc, iloc)](https://teddylee777.github.io/pandas/pandas-tutorial-03)
```python
import pandas as df

queryset = <테이블 모델>.query.filter(<테이블 모델>.<테이블 컬럼>.like('%'+search_text+'%'))
또는
queryset = db.session.query(<테이블 명 또는 컬럼>).filter(<테이블 모델>.<테이블 컬럼>.like('%'+search_text+'%'))

# 중요한 점은 .all() .first() 등 결과 객체를 반환하지 않고 sql 객체 그대로 pandas.read_sql()에 전달

df = pd.read_sql(queryset.statement, queryset.session.bind)
# pd.read_sql(queryset.statement, <세션바인드 멀티 DB일 경우 해당 DB 세션을 연결 예. db.get_engine(app, bind명)>)


# 기본출력은 a:[], b:[], c:[] 이고 뒤에 orient='records'옵션을 추가하면 [{a:'',b:'',c:''},{a,b,c..},{}] 형태로 변환

print(json.loads(df.to_json(orient='records')))
```
* [subquery](https://stackoverrun.com/ko/q/10713483)
* [autocommit](https://ash84.io/2018/07/30/sqlalchemy-autocommit/)

* ORM 방식 쿼리와 기본 쿼리 방식의 트랜젝션을 공유하지 않음.


```python
 # 특정 컬럼값만 리스트로 출력
 df = pd.real_sql(<sql_data>.statement, <sql_data>.session.bind)
 data = df['컬럼명'].to_numpy()
 
```


# other
```
mac os13 update 후 postgresql 빌드 오류 시
sudo ln -s /opt/homebrew/opt/postgresql@14/lib/postgresql@14/libpq.5.dylib /usr/local/lib/libpq.5.dylib

```

