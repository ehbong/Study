# kubernetes

* [kubernetes 공식문서](https://kubernetes.io/ko/docs/home/)
* [도커를 대체하는 컨테이너 관리 podman](https://podman.io/)


#### cli 명령어
> 규칙
> * kubectl 로 시작
> * - 와 사용하는 옵션은 단일 알파벳,숫자와 함께 사용, 짧은옵션
> * -- 와 사용하는 옵션은 알파벳 두글자 이상으로 구성, 긴 옵션
> * 
```bash

## kubectl run 파드이름 --image=이미지이름 --port=포트번호
$ kubectl run nginx --image=nginx
```
