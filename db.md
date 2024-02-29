## DB

### Index
* [index 란?](https://itholic.github.io/database-index/)
* [index 장단 및 생성전략](https://coding-factory.tistory.com/746)
* [B-tree 에 대한 설명 유튜브](https://youtu.be/bqkcoSm_rCs)
* [B-tree, B+tree 차이](https://ssocoit.tistory.com/217)

#### 최대 연결 수, 커넥션 풀
> * DB 설정에 최대 연결 수와, WAS에서 커넥션 관리 객체가 생성하는 커넥션 풀  
> * 최대 연결 수는 DB와 연결을 맺고 있는 서버들의 커넥션 기본 연결 수를 더한 값보다 높게 권장  
> * WAS 에서 커넥션 풀이 가득 찼을 경우 설정한 대기 시간동안 대기 했다가, 지나면 오류 발생  

### 분산처리
* [파티셔닝, 샤딩, 레플리케이션 설명](https://youtu.be/P7LqaEO-nGU)
```markdown
 * partitioning
   DB 데이터 저장공간을 분리하는 방법
   1. vertical partitioning
      * 컬럼을 기준으로 테이블을 나누는 방식(정규화, 데이터가 많은 컬럼을 분리 등)
   2. horizontal partitioning
      * 로우를 기준으로 테이블을 나누는 방식
      * 특정 컬럼을 기준으로 잡고 해시함수 또는 범위를 기준으로 데이터를 나눔 비지니스 모델에서
        가장많이 사용되는 데이터를 사용하는 키(파티션키)로 선정 필요
      * 데이터를 잘 균등하게 분배될 수 있도록 하는 것도 중요
      * 해시함수를 활용한 파티셔닝은 한번 파티셔닝 후 파티션 추가가 어려움
 * sharding
   각 파티션들을 서로 다른 DB서버에 저장해서 부하분산을 하는 방법
 * replication
   주와 부 DB서버를 생성해서 DB장애 대응 및 부하 분산을 하는 방법
```
* [단계별 정규화](https://minimax95.tistory.com/entry/%EC%A0%95%EA%B7%9C%ED%99%94Normalization-%EA%B0%9C%EB%85%90%EA%B3%BC-%EA%B8%B0%EB%B3%B8-%EA%B3%BC%EC%A0%95)
* [SQL query 튜닝](https://cornswrold.tistory.com/87)
* [실행계획을 노드로 변환 해주는 페이지](https://explain.dalibo.com/)

* [stored function](https://youtu.be/I1jjR58Rzic)
* [stored procedure](https://youtu.be/I1jjR58Rzic)
* [무료 ERD ERDCLOUD](https://www.erdcloud.com/)
* [DB네이밍 팁](https://jang8584.tistory.com/35)
* [DBeaver 에서 실행계획 보는법](http://item.gmarket.co.kr/detailview/item.asp?goodscode=2267277866)
* [DB 옵티마이저란?](https://coding-factory.tistory.com/743)
* [couchebase db 개념과 특징](https://azderica.github.io/02-db-nosql-couchbase/)
* [aws db 데이터 마이그레이션](https://aws.amazon.com/ko/dms/)
* [효과적인 nosql 활용 feat AWS](https://www.youtube.com/watch?v=8rEsuvdL17s) 
* [connection pool 연결 지연 대기](https://engineering-skcc.github.io/cloud/tomcat/apache/DB-Pool-For-Event/)
* [n+1문제 이슈](https://fouaaa.blogspot.com/2021/06/n1.html)
```python
 # 주로 orm 을 사용하여 데이터를 불러올 때 발생하며, 반복문 등으로 데이터를 불러올 때 발생
from sqlalchemy.orm import sessionmaker

Session = sessionmaker(bind=engine)
session = Session()
   
# 사용자 목록을 가져옴
users = session.query(User).all()
   
# 각 사용자별로 주문 목록을 가져옴
for user in users:
    # 사용자별 주문을 n개 만큼 select 쿼리를 실행해서 부하를 발생시킴 
    orders = user.orders
# join을 사용해서 대응

```
* [트랜잭션의 격리 수준(isolation Level)이란?](https://nesoy.github.io/articles/2019-05/Database-Transaction-isolation)
* [transaction isolation level 유튜브 설명](https://youtu.be/bLLarZTrebU)
```markdown
1. 이상현상
 * dirty read
   하나의 트랜젝션에서 같은 데이터를 2번 읽어오는 와중에 다른 트랜젝션에서 커밋되지 않은 데이터 변경으로 인해
   다른 데이터가 반환됨
 * nonrepeatable read
   하나의 트랜젝션에서 같은 데이터를 2번 읽어오는 와중에 다른 트랜젝션의 데이터 변경 커밋으로 인해
   다른 데이터가 반환됨
 * phantom read
   하나의 트랜젝션의 조건에 데이터를 2번 읽어오는 와중에 다른 트랜젝션의 데이터 변경 커밋으로 인해
   조건에 맞는 데이터가 변경 됨
   ex) A=10 >> 1건, 다른트랜젝션에서 데이터 변경, A=10 >> 2건
2. isolation level
   대응 단계가 높을 수록 동시성이 떨어져서 데이터베이스 처리속도에 영향있음
 1. read uncommitted
   위의 이상현상 3개를 전부 허용
 2. read committed
   drity read 만 허용하지 않음
 3. repeatable read
   drity read, nonrepeatable read를 허용하지 않음
 4. serializable
   모든 이상현상을 허용하지 않음
 ** snapshot isolation 위 대응 단계와 별개의 단계
   트랜젝션 시작지점에서 snapshot을 찍어서 해당 시점 기준 데이터를 가져와서 반환함
   같은 데이터를 2개이상의 트랜젝션이 변경요청 할 경우 먼저 commit된 데이터만 반영되고, 이후는 반영되지 않음
```

## NoSQL
* [데이터 모델링 형태 별 특징](https://bcho.tistory.com/665)
* [MongoDB 집계(그룹)](https://spidyweb.tistory.com/190)
* [MongoDB 특징](https://inpa.tistory.com/entry/MONGO-%F0%9F%93%9A-%EB%AA%BD%EA%B3%A0%EB%94%94%EB%B9%84-%ED%8A%B9%EC%A7%95-%EB%B9%84%EA%B5%90-%EA%B5%AC%EC%A1%B0-NoSQL#%EC%8B%A0%EB%A2%B0%EC%84%B1reliability)

## Elastic Search
* [Elastic Search 공식](https://www.elastic.co/kr/elasticsearch/)
* [Elastic Search 기본 설명 및 장단점](https://jaemunbro.medium.com/elastic-search-%EA%B8%B0%EC%B4%88-%EC%8A%A4%ED%84%B0%EB%94%94-ff01870094f0)
* [Elastic Search와 MySQL 연동](https://m.blog.naver.com/olpaemi/221644176875)

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
* [PostgreSQL vs MySQL 쓰기 방식 차이](https://velog.io/@zihs0822/PostgreSQL-vs-MySQL-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%93%B0%EA%B8%B0-%EB%B0%A9%EC%8B%9D)
* [더미데이터 적용 방법](https://feellikeghandi.tistory.com/17)
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
> 조건부 인덱스
```sql
-- 아래 SQL처럼 조건부로 인덱스를 작성 가능
-- 조건부 인덱스의 경우 일정구간만 인덱싱해서 인덱싱 비용 절감
-- 인덱스에서 제외된 컬럼 값이 자주 변경되면 인덱스 관리 비용이 상승함
CREATE INDEX my_index ON my_table (my_column) WHERE my_column >= 100;
```
* [PostgreSQL Replication 설명](https://feellikeghandi.tistory.com/18)


## 인메모리 DB
* [redis 공식문서](https://redis.io/docs/about/)
* [redis 설명](https://devlog-wjdrbs96.tistory.com/374)
```bash
# cli 명령어
# 진입
redis-cli
# 원격 진입
redis-cli -h 호스트 -p 포트

# string 키, 값 입출력
# set <키> <값>, get <키>
set a 1
get a

# 키 배열을 순환해서 반환
# keys 명령어는 한번에 모든 키를 찾아 반환하므로
# 동작하는 동안 시스템이 멈춤
# scan은 iterater 방식으로 스케줄링되어
# 사용 권장
# 0일 경우 전체 반복 스캔
# 자세한 내용은 https://redis.io/commands/scan/ 참고
scan 0
# Set 유형의 요소 반환
sscan key 0
# 해시맵 유형의 요소 반환
hscan key 0 
# Sorted set 유형의 요소 반환
zscan key 0

# 리스트 자료형 https://redis.io/docs/data-types/lists/
# 왼쪽으로 데이터 삽입
lpush key value
# 오른쪽으로 데이터 삽입
rpush key value

# 왼쪽, 오른쪽 데이터 추출(추출된 데이터 제거)
lpop key
rpop key

# set 자료형 https://redis.io/docs/data-types/sets/
# 데이터 삽입
# 한칸씩 간격을 추가해서 하나이상의 데이터를 삽입
sadd key value value2 value3 ...
# 해당 set에 있는 객체를 반환
smembers key
# 해당 값이 있는 지 확인 있으면 1 없으면 0
sismember key value
# 값 수 반환
scard key
# 정해진 수만큼 값 추출(추출된 데이터 제거)
spop key count


# hesh map 자료형 https://redis.io/docs/data-types/hashes/
# 데이터 삽입
hset key 내부key value
# 데이터 조회
hget key 내부key
# 내부 key 수 반환
hlen key
# 내부 key 모두 반환
hkeys key
# 내부 value 모두 반환
hvals key

```
* [Python에서 Redis를 사용](https://soyoung-new-challenge.tistory.com/117)
* [pub/sub python예제](https://snowdeer.github.io/python/2021/12/22/python-redis-pubsub-example/)
* [pub/sub 설명](http://redisgate.kr/redis/command/pubsub_intro.php)
* [docker로 생성하여 연결할때 conf 파일 수정 값](https://stackoverflow.com/questions/62162222/redis-connection-refused-between-containers)
```
 bind 127.0.0.1 # 주석처리
 protected-mode no # yes -> no
```
* [Kafka와 Redis의 pub/sub 차이](https://medium.com/frientrip/pub-sub-%EC%9E%98-%EC%95%8C%EA%B3%A0-%EC%93%B0%EC%9E%90-de9dc1b9f739)

## 메시지 브로커
###### Kafka
* [Kafka 설명](https://galid1.tistory.com/793)
* [Kafka 주요개념 및 용어](https://ifuwanna.tistory.com/487)
* [Kafka 유튜브 설명](https://youtu.be/0Ssx7jJJADI)
프로듀서(Producer)
> * 메시지 생산자
> * 데이터를 토픽(Topic)이란 단위로 분류하고 전송

컨슈머(Consumer)
> * 메시지 소비자
> * 컨슈머 그룹에 속함
> * 한개의 파티션은 컨슈머 그룹의 하나의 컨슈머만 연결 가능

토픽(Topic)
> * 데이터가 저장되는 카테고리
> * 프로듀서를 통해 데이터를 받으며, 컨슈머(Consumer)에게 메시지를 전달
> * 1개 이상의 파티션으로 나뉘어짐

파티션(Partition)
> * 토픽의 물리적 저장단위
> * 1개 이상의 브로커에 분산 저장
> * append-only(설정에 따라 일정 시간이 지난 뒤 삭제)

브로커(Broker)
> * 데이터를 저장, 관리하는 역할
> 주키퍼(ZooKeeper)
> * 브로커의 상태, 토픽 구성 컨슈머 그룹 정보등을 관리

리밸런스(rebalance)
> 컨슈머 그룹의 파티션 소유권 변경이 발생할 때 발생
> * consumer.close() 호출 또는 세션이 끊겼을 때 발생(명시적 종료 및 Heartbeat 미전송에 따른 세션 타임 아웃)
> * 데이터 유실 및 중복 발생 가능(commitSync 또는 추가적인 방법 필요)

컨슈머 랙(Consumer lag)
> 토픽의 마지막 오프셋과 컨슈머 마지막 커밋 오프셋의 차
> * 컨슈머 랙이 쌓이면, 프로듀서의 이벤트 발행보다 컨슈머의 이벤트 처리가 늦다는 의미

옵션
> ***Consumer Option***
> enable.auto.commit(true/false)
> * true: 일정간격(auto.commit.interval.ms). poll() 메서드 호출시 자동 commit
> 	* 속도가 빠름
> 	* 중복 또는 유실이 발생할 수 있음(중복/유실이 허용되지 않는 곳에서는 사용 금지)
> * flase: 직접 커밋 메서드를 호출
> 	* commitSync(): 동기 커밋
> 		* 레코드 처리 순서 보장
> 		* 커밋이 완료될 때 까지 block(가장 느림)
> 		* poll 메서드로 반환된 마지막 레코드의 오프셋을 커밋하거나, 특정 오프셋 지정 커밋
> 	* commitAsync(): 비동기 커밋
> 		* 중복이 발생 가능(네트워크 문제로 이전 offset보다 이후 offset이 먼저 커밋될 떄)
> 		* 레코드 처리 순서를 보장하지 못함(처리 순서가 중요한 서비스에서는 사용 제한)
> 
## 데이터 웨어하우스
* [OLTP, OLAP 비교](https://too612.tistory.com/511)
* [Snowflake, BigQuery, Redshift 비교](https://giljae.medium.com/snowflake-bigquery-redshift-%EB%B9%84%EA%B5%90-5c585df450b7)

