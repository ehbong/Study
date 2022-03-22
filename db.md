# DB

* [index 란?](https://itholic.github.io/database-index/)
* [mysql 암복호화 AES_ENCRYPT & AES_DECRYPT](https://stricky.tistory.com/330)
* [단계별 정규화](https://minimax95.tistory.com/entry/%EC%A0%95%EA%B7%9C%ED%99%94Normalization-%EA%B0%9C%EB%85%90%EA%B3%BC-%EA%B8%B0%EB%B3%B8-%EA%B3%BC%EC%A0%95)
* [SQL query 튜닝](https://cornswrold.tistory.com/87)
* [mysql 세부 설정](https://happist.com/577204/db-%ED%8A%9C%EB%8B%9D%EC%9C%BC%EB%A1%9C-mysql-%EC%B5%9C%EC%A0%81%ED%99%94)
* [mysql query cache 설정](https://jupiny.com/2021/01/10/mysql-query-cache-disadvantage/)
* [무료 ERD ERDCLOUD](https://www.erdcloud.com/)
* [DB네이밍 팁](https://jang8584.tistory.com/35)

* [aws db 데이터 마이그레이션](https://aws.amazon.com/ko/dms/)

> mysql 데드락 걸렸을때 대처
```sql
# 프로세스 확인
SHOW PROCESSLIST;
# 상태가 Waiting for table metadata lock 일 경우
KILL <PROCESS ID>
# innodb의 상태 확인
SHOW ENGINE INNODB STATUS;
```

## PostgreSQL

* [Aurora MySQL vs Aurora PostgreSQL](https://techblog.woowahan.com/6550/)
* [postgreSQL 특장점](https://codecamp.tistory.com/2)
* [PostgreSQL 쿼리 속도 개선](https://hyperconnect.github.io/2020/08/31/improve-slow-query.html)
* [postgresql AUTO INCREMENT](https://aspdotnet.tistory.com/2401)
* [join 종류](https://venova.tistory.com/entry/SQL-PostgreSQL-Join-%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C)
* [parttioning](https://hides.tistory.com/1040)
* [선언적파티셔닝, 상속 파티셔닝](https://uiandwe.tistory.com/1318)
* [성능개선 방법](https://uiandwe.tistory.com/1283)

## 인메모리 DB
* [redis](https://aws.amazon.com/ko/elasticache/what-is-redis/)
* [Python에서 Redis를 사용](https://soyoung-new-challenge.tistory.com/117)
