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

* [func 함수에 대해](https://item4.blog/2015-07-05/Internal-of-sqlalchemy.sql.expression.func/)

* [동적쿼리1](https://stackoverflow.com/questions/37336520/sqlalchemy-dynamic-filter)

* [동적쿼리2](https://stackoverrun.com/ko/q/10784033)

* [nvl 역할을 하는 func.coalesce](https://programtalk.com/python-examples/sqlalchemy.sql.func.coalesce/)

* [in 조건](https://stackoverflow.com/questions/8603088/sqlalchemy-in-clause)

* [특정 컬럼만 출력](https://qastack.kr/programming/11530196/flask-sqlalchemy-query-specify-column-names)

* [테이블 별칭 & 조인](https://edykim.com/ko/post/getting-started-with-sqlalchemy-part-2/)

* [pandas로 데이터 출력](https://lemontia.tistory.com/844)
```
import pandas as df

queryset = stock.query.filter(stock.name.like('%'+search_text+'%'))

# 위와 달라진게 있다면 끝에 .all() 이 없다 (sql 객체 그대로 pandas.read_sql()에 전달)

df = pd.read_sql(queryset.statement, queryset.session.bind)


# 기본출력은 a:[], b:[], c:[] 이고 뒤에 orient='records'옵션을 추가하면 [{a:'',b:'',c:''},{a,b,c..},{}] 형태로 변환

print(json.loads(df.to_json(orient='records')))
```

