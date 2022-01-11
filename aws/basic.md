# AWS BASIC
* [AWS 기본 교육](https://kr-id-general.workshop.aws/ko/compute/launching.html)
* [AWS cluoud 보안 교육](https://www.aws.training/Details/eLearning?id=54772)
* [AWS EC2 putty 로 접속](https://mozi.tistory.com/191)
* [결제 대시보드](https://console.aws.amazon.com/billing/home?region=ap-northeast-2#/)
* [VPC 개념이해하기](https://medium.com/harrythegreat/aws-%EA%B0%80%EC%9E%A5%EC%89%BD%EA%B2%8C-vpc-%EA%B0%9C%EB%85%90%EC%9E%A1%EA%B8%B0-71eef95a7098)

* [CloudFront 함수생성](https://docs.aws.amazon.com/ko_kr/AmazonCloudFront/latest/DeveloperGuide/edge-functions.html)
* [CloudFront 함수생성 예제](https://github.com/aws-samples/amazon-cloudfront-functions)
>  CloudFront 는 ECMAScript (ES) version 5.1 을 준수

## VPC
* [VPC 공식문서](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/what-is-amazon-vpc.html)
* [VPC 쉽게 이해하기](https://medium.com/harrythegreat/aws-%EA%B0%80%EC%9E%A5%EC%89%BD%EA%B2%8C-vpc-%EA%B0%9C%EB%85%90%EC%9E%A1%EA%B8%B0-71eef95a7098)


## EC2
* [Ec2 속도저하](https://steemit.com/kr-dev/@segyepark/aws-ec2)
* [stmp 포트 제한 제거 요청 방법](https://support.bespinglobal.com/support/solutions/articles/16000041126--aws-ec2-smtp-25-)
* [Smtp 포트 여는 방법 (기본적으로 EC2는 smtp 포트가 막힘)](https://aws.amazon.com/ko/premiumsupport/knowledge-center/ec2-port-25-throttle/)
* Ec2 인스턴스 생성시 gp2볼륨은 크기별로 IOPS(입출력제한)가 달라짐. 사용용량이 작은데 입출력이 많을 경우 gp3볼륨으로 변경. 사용가능IOPS를 초과하면 인스턴스가 느려지거나 접속불가.
* EC2 종료는 인스턴스의 삭제를 의미하므로 종료 방지 설정 필수
* [EBS 볼륨은 IO 제한이 존재하고 gp2의 경우 gp3로 마이그래이션가능하다](https://aws.amazon.com/ko/blogs/korea/new-amazon-ebs-gp3-volume-lets-you-provision-performance-separate-from-capacity-and-offers-20-lower-price/)
* [Session Manager를 이용한 접속](https://eunsu-shin.medium.com/aws-ssm-session-manager-%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%98%EC%97%AC-ec2-%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%EC%97%90-%EC%A0%91%EC%86%8D%ED%95%98%EA%B8%B0-14d52de21a3c)
* EC2 무제한모드(일부 인스턴스기능) 설정 방법
  1. 인스턴스 선택
  2. 마우스 우클릭
  3. 인스턴스 설정
  4. 크래딧 사양변경
* [인스턴스 경보 만들기](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/using-cloudwatch-createalarm.html)
##### 인스턴스 유형
 * 마이크로(T)
    * 인스턴스 크기별 기본 수준의 CPU 성능 제공
    * 일정 %의 이상을 CPU사용량이 꾸준히 있으면 크레딧을 소모해서 인스턴스에 쓰로틀링이 발생 후 다운(***운영에 적합하지 않음)
      (휴대폰 요금제처럼 사용량에 따라 크레딧을 소모를 하고 크레딧을 전부 소모시 쓰로틀링이발생)
    * 간헐적으로 높은 성능이 필요할 때 유휴시간에 모아 놓은 크레딧을 기반으로 버스팅하여 높은 성능을 제공
    * 적용사례 : 개발환경, 소규모 웹, 마이크로 서비스
 * 범용(M)
    * 컴퓨팅, 메모리 및 네트워크 리소스를 균형 있게 제공
    * 적용사례 : 중소형 DB, 기타 엔터프라이즈 애플리케이션 
 * 컴퓨팅 최적화(C) 연산집약
    * 가장 높은 수준의 컴퓨팅 성능을 제공
    * 적용사례 : 고성능 프론트 엔드, 웹서버, 배치(일괄처리), 게임
 * 스토리지 최적화(I)
    * SSD 기반의 초고속 랜던 I/O 성능에 최적화된 인스턴스 스토리지 제공
    * 적용사례 : NoSQL DB, DW(data warehouse), 하둡 및 분산 시스템
 * 스토리지 최적화(D)
    * HDD 기반 높은 디스크 처리량 제공
    * 적용사례 : MPP DW(대용량병렬처리 DW), MapReduce(분산 병렬 컴퓨팅)
 * 메모리 최적화(X)
    * 인-메모리 DB. 메모리 기반의 빅 데이터 처리 엔진 및 HPC(고성능 컴퓨팅) 애플리케이션에 적합
    * 적용사례 : SAP HANA, Apache Spark, Presto
 * 메모리 최적화(R)
    * 적용사례 : 고성능 DB, 분산 메모리 캐시, 게놈 분석
 * 가속화된 컴퓨팅(G, P, F)
    * GPU 및 FPGA를 이용한 높은 컴퓨팅 애플리케이션
    * 적용사례 : 3D 앱 스트리밍, ML


## IAM
* IAM 권한설정. 
  * 인라인 정책 : 그룹 또는 사용자에게 정책을 직접 부여하는 방식으로 해당 정책 삭제 시 소멸.
  * 관리형 정책 : 정책을 생성 후 그룹 또는 사용자에게 연결 시키는 방식. 연결으 해제해도 정책은 유지.


## ElastiCache
* [ElastiCache와 Redis를 이용한 세션클러스터](https://aws.amazon.com/ko/getting-started/hands-on/building-fast-session-caching-with-amazon-elasticache-for-redis/)

## 탄력적 IP(고정IP)
* [탄력적 IP기본 갯수(5개) 이상으로 늘리고 싶을때](https://goodlife-coding.tistory.com/entry/Elastic-IP%ED%83%84%EB%A0%A5%EC%A0%81-IP-%ED%95%A0%EB%8B%B9-%ED%95%9C%EA%B3%84-%EB%B0%8F-%EC%9A%94%EA%B8%88-%EB%B6%80%EA%B3%BC-%EB%B0%A9%EC%8B%9D)
```
  1. support
  2. support center 
  4. Create case 
  5. Regarding : Service Limit Increase 
  6. Limit Type : Elastic IPs 
  7. 리전 선택(서울리전) 
  8. limit 개수 수정
```


#### 서브도메인 생성 및 SSL 인증서 적용
* [Route 53 서브 도메인 공식문서](https://aws.amazon.com/ko/premiumsupport/knowledge-center/create-subdomain-route-53/)
* [AWS 서브 도메인 설정](https://blog.self-made.cloud/232)
> 서브도메인 생성
> > 호스팅영역 생성 없이 레코드만 추가해서 서브 도메인 추가 시 SSL 인증서 적용이 안됨.(인증서에 등록된 주소와, 서브 도메인 주소가 다름으로)
1. [AWS 호스팅영역 생성](https://console.aws.amazon.com/route53/v2/hostedzones#) 서브 도메인 명으로 생성
2. 생성된 서브도메인의 NS 값을 복사 
3. 메인 도메인에 레코드 생성, 레코드 이름은 서브도메인명, 레코드 유형 NS, 값은 2번에서 복사한 NS값을 넣음
4. 서브도메인 호스팅 영역에 레코드 생성해서 대상 연결 및 SSL 설정
5. 서브도메인에서는 일부 레코드는 추가 되지 않음 
