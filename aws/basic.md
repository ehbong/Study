# AWS BASIC
* [AWS 기본 교육](https://kr-id-general.workshop.aws/ko/compute/launching.html) 

## VPC

* [VPC 쉽게 이해하기](https://medium.com/harrythegreat/aws-%EA%B0%80%EC%9E%A5%EC%89%BD%EA%B2%8C-vpc-%EA%B0%9C%EB%85%90%EC%9E%A1%EA%B8%B0-71eef95a7098)


## EC2
* [Ec2 속도저하](https://steemit.com/kr-dev/@segyepark/aws-ec2)
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

## IAM
* IAM 권한설정. 
  * 인라인 정책 : 그룹 또는 사용자에게 정책을 직접 부여하는 방식으로 해당 정책 삭제 시 소멸.
  * 관리형 정책 : 정책을 생성 후 그룹 또는 사용자에게 연결 시키는 방식. 연결으 해제해도 정책은 유지.
