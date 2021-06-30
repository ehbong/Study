# SQLAlchemy

## 파이썬 ORM 모듈

### 설치방법

```
  pip3 install sqlalchemy
```


* [SQLAlchemy 공식사이트](https://www.sqlalchemy.org/)

* [SQLAlchemy 튜토리얼](https://riptutorial.com/ko/sqlalchemy)

* [SQLAlchemy 튜토리얼 번역](https://edykim.com/ko/post/getting-started-with-sqlalchemy-part-1/)

* [flask_sqlalchemy](https://opentutorials.org/module/3669/22070)

* [SQLAlchemy SQL 호출예제](https://lowelllll.github.io/til/2019/04/19/TIL-flask-sqlalchemy-orm/)

* [이미 있는 DB의 모델정보 가져오기](https://beomi.github.io/2017/10/20/DB-To-SQLAlchemy-Model/)
```
  # 디비 모델 정보 가져오기
  pip install flask-sqlacodegen
  flask-sqlacodegen "mysql://username:password@DB_IP/DB_NAME" --flask > models.py
```

* [func 함수에 대해](https://item4.blog/2015-07-05/Internal-of-sqlalchemy.sql.expression.func/)

* [동적쿼리1](https://stackoverflow.com/questions/37336520/sqlalchemy-dynamic-filter)

* [동적쿼리2](https://stackoverrun.com/ko/q/10784033)

* [nvl 역할을 하는 func.coalesce](https://programtalk.com/python-examples/sqlalchemy.sql.func.coalesce/)

* [in 조건](https://stackoverflow.com/questions/8603088/sqlalchemy-in-clause)

* [특정 컬럼만 출력](https://qastack.kr/programming/11530196/flask-sqlalchemy-query-specify-column-names)

* [테이블 별칭 & 조인](https://edykim.com/ko/post/getting-started-with-sqlalchemy-part-2/)

* [Hybrid Attributes 공식문서](https://docs.sqlalchemy.org/en/13/orm/extensions/hybrid.html) 

* [Hybrid Attributes를 이용한 암호화](https://spoqa.github.io/2011/12/10/sqlalchemy-hybrid-attributes.html)
* [여러 DB를 사용중일때 특정 연결(엔진)을 불러올때](https://github.com/pallets/flask-sqlalchemy/issues/359)
```
##여러 DB를 사용중일때 특정 연결(엔진)을 불러올때
 db.get_engine(app, <bind명>)
```

# Pandas
* [pandas](http://pythonstudy.xyz/python/article/408-pandas-%EB%8D%B0%EC%9D%B4%ED%83%80-%EB%B6%84%EC%84%9D)
* [pandas로 데이터 출력](https://lemontia.tistory.com/844)
```
import pandas as df

queryset = stock.query.filter(stock.name.like('%'+search_text+'%'))

# 위와 달라진게 있다면 끝에 .all() 이 없다 (sql 객체 그대로 pandas.read_sql()에 전달)

df = pd.read_sql(queryset.statement, queryset.session.bind)
# pd.read_sql(queryset.statement, <세션바인드 멀티 DB일 경우 해당 DB 세션을 연결 예. db.get_engine(app, bind명)>)


# 기본출력은 a:[], b:[], c:[] 이고 뒤에 orient='records'옵션을 추가하면 [{a:'',b:'',c:''},{a,b,c..},{}] 형태로 변환

print(json.loads(df.to_json(orient='records')))
```
* [subquery](https://stackoverrun.com/ko/q/10713483)
* [autocommit](https://ash84.io/2018/07/30/sqlalchemy-autocommit/)

* ORM 방식 쿼리와 기본 쿼리 방식의 트랜젝션을 공유하지 않음.


```
 # 특정 컬럼값만 리스트로 출력
 df = pd.real_sql(<sql_data>.statement, <sql_data>.session.bind)
 data = df['컬럼명'].to_numpy()
 
```


