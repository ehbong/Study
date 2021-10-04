# AWS CLI

* [AWS CLI 공식문서](https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/cli-chap-welcome.html)

* [AWS CLI 설치 for Linux](https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/install-cliv2-linux.html)


#### AWS CLI 기본 설치 및 설정

1. iam 사용자 생성
2. iam 권한설정
3. [iam 액세스 키 ID 및 보안 액세스 키](https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-creds)
4. ec2 접속
5. AWS cli 설치(최신 버전 설치)
```bash
$ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```
6. [aws configure를 통한 빠른 구성](https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-config)
```bash
$ aws configure
AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: us-west-2
Default output format [None]: json
```


#### AWS CLI 보안 그룹 설정
###### [보안 그룹 생성](https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/cli-services-ec2-sg.html#creating-a-security-group)
```bash
$ aws ec2 create-security-group --group-name <그룹이름> --description "<그룹설명>" --vpc-id <VPC 아이디>
```

###### [보안 그룹에 규칙 추가](https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/cli-services-ec2-sg.html#configuring-a-security-group)
```bash
$ aws ec2 authorize-security-group-ingress --group-id <보안그룹ID> --protocol tcp --port <허용포트> --cidr <IP 예 192.0.0.1/32 모두 허용일 경우 0.0.0.0/0>
```

###### 보안 그룹 내용 확인
```bash
$ aws ec2 describe-security-groups --group-ids <보안그룹ID>
```

###### [보안 그룹 삭제](https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/cli-services-ec2-sg.html#deleting-a-security-group)
```bash
$ aws ec2 delete-security-group --group-id <보안그룹ID>
```

###### [보안 그룹에 IP 삭제](https://docs.aws.amazon.com/cli/latest/reference/ec2/authorize-security-group-ingress.html)
```bash
## 정보로 삭제
$ aws ec2 revoke-security-group-ingress --group-id <보안그룹ID> --protocol tcp --port <허용포트> --cidr <IP 예 192.0.0.1/32 모두 허용일 경우 0.0.0.0/0>
## security-group-rule-ids 로 삭제
$ aws ec2 revoke-security-group-ingress --group-id <보안그룹ID> --security-group-rule-ids <보안그룹 규칙ID>
```
