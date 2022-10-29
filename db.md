## DB

* [index 란?](https://itholic.github.io/database-index/)
* [단계별 정규화](https://minimax95.tistory.com/entry/%EC%A0%95%EA%B7%9C%ED%99%94Normalization-%EA%B0%9C%EB%85%90%EA%B3%BC-%EA%B8%B0%EB%B3%B8-%EA%B3%BC%EC%A0%95)
* [SQL query 튜닝](https://cornswrold.tistory.com/87)
* [무료 ERD ERDCLOUD](https://www.erdcloud.com/)
* [DB네이밍 팁](https://jang8584.tistory.com/35)
* [DBeaver 에서 실행계획 보는법](http://item.gmarket.co.kr/detailview/item.asp?goodscode=2267277866)
* [couchebase db 개념과 특징](https://azderica.github.io/02-db-nosql-couchbase/)
* [aws db 데이터 마이그레이션](https://aws.amazon.com/ko/dms/)
* [효과적인 nosql 활용 feat AWS](https://www.youtube.com/watch?v=8rEsuvdL17s) 
* [connection pool 연결 지연 대기](https://engineering-skcc.github.io/cloud/tomcat/apache/DB-Pool-For-Event/)
* [n+1문제 이슈](https://fouaaa.blogspot.com/2021/06/n1.html)

## mysql
* [mysql 암복호화 AES_ENCRYPT & AES_DECRYPT](https://stricky.tistory.com/330)
* [mysql 세부 설정](https://happist.com/577204/db-%ED%8A%9C%EB%8B%9D%EC%9C%BC%EB%A1%9C-mysql-%EC%B5%9C%EC%A0%81%ED%99%94)
* [mysql query cache 설정](https://jupiny.com/2021/01/10/mysql-query-cache-disadvantage/)
* [mysql timeout setting, sleep session 정리](https://sarc.io/index.php/mariadb/1154-sleep-session)

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
* [PostgreSQL 쿼리 튜닝](https://velog.io/@doohyunlm/DB-SQL-%ED%8A%9C%EB%8B%9D)
* [postgresql AUTO INCREMENT](https://aspdotnet.tistory.com/2401)
* [query timeout 설정](https://jojoldu.tistory.com/631)
* [join 종류](https://venova.tistory.com/entry/SQL-PostgreSQL-Join-%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C)
* [partitioning](https://hides.tistory.com/1040)
* [선언적파티셔닝, 상속 파티셔닝](https://uiandwe.tistory.com/1318)
* [postgreSQL 성능개선 방법](https://uiandwe.tistory.com/1283)
* [실행계획 분석](https://seungtaek-overflow.tistory.com/5)
* [postgis 위치 정보](https://postgis.net/)
* [json type 사용 방법](https://brownbears.tistory.com/504)
* [postgresql 실행 계획 분석, 상황별 실행되는 스캔](https://seungtaek-overflow.tistory.com/5)
* [PostgreSQL synchronous_commit](http://minsql.com/postgres/PostgreSQL-synchronous_commit-%EA%B0%9C%EB%85%90%EB%8F%84/)
* [autovacuum 튜닝](https://nrise.github.io/posts/postgresql-autovacuum/)
* [blocking query 확인 및 킬 방법](https://aws.amazon.com/ko/premiumsupport/knowledge-center/dms-error-canceling-statement-timeout/)
* [pg_cron을 활용한 배치](https://docs.aws.amazon.com/ko_kr/AmazonRDS/latest/UserGuide/PostgreSQL_pg_cron.html)
* [deadlock 확인 및 해결방법](https://aws.amazon.com/ko/premiumsupport/knowledge-center/rds-aurora-postgresql-query-blocked/)
* [숫자타입 데이터 특징](https://www.devkuma.com/docs/postgresql/%EC%88%AB%EC%9E%90-%ED%98%95%EC%8B%9D-integer-decimal-double-precision-%EB%93%B1/)
* [case when 조건 값](https://mine-it-record.tistory.com/418)
* [정규식 이용 방법](https://iyabong.tistory.com/entry/DB-%EC%A0%95%EA%B7%9C%EC%8B%9D-PostgreSQL-%EC%BD%94%EB%93%9C%ED%92%88%EB%AA%85-%EB%AC%B8%EC%9E%90%EC%97%B4%EC%97%90%EC%84%9C-%EC%BD%94%EB%93%9C-%EC%B6%94%EC%B6%9C%ED%95%98%EA%B8%B0)
```SQL
# 정규식 예제
SUBSTRING(<컬럼명> FROM '<정규식>')
```

## 인메모리 DB
* [redis](https://aws.amazon.com/ko/elasticache/what-is-redis/)
* [redis 설명](https://devlog-wjdrbs96.tistory.com/374)
* [Python에서 Redis를 사용](https://soyoung-new-challenge.tistory.com/117)
* [단계별 redis 설명](https://velog.io/@devsh/Redis-1-Redis%EB%9E%80)
* [pub/sub python예제](https://snowdeer.github.io/python/2021/12/22/python-redis-pubsub-example/)
* [pub/sub 설명](http://redisgate.kr/redis/command/pubsub_intro.php)
* [docker로 생성하여 연결할때 conf 파일 수정 값](https://stackoverflow.com/questions/62162222/redis-connection-refused-between-containers)
```
 bind 127.0.0.1 # 주석처리
 protected-mode no # yes -> no
```
