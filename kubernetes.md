# kubernetes

* [kubernetes 공식문서](https://kubernetes.io/ko/docs/home/)
* [도커를 대체하는 컨테이너 관리 podman](https://podman.io/)


#### cli 명령어
> 규칙
> * kubectl (command) (TYPE) (NAME) (flags) 구조
> 	* command: 수행하려는 동작에 맞는 명령어
> 		* apply: 상태 적용
> 		* get: 지정한 타입의 리소스 조회
> 		* describe: 리소스 상태 상세 조회
> 		* delete: 리소스 제거
> 		* logs: 로그 조회
> 		* exec: 컨테이너 명령어 전달
> 		* config: 설정관리
> 		* run: 클러스터에서 지정된 이미지를 실행(없으면 설치 후 실행)
> 	* TYPE: 리소스 타입 (pod, pods, services)
> 	* NAME: 리소스 이름
> 	* flags: 옵션 값
> 		* - 와 사용하는 옵션은 단일 알파벳,숫자와 함께 사용, 짧은옵션
> 		* -- 와 사용하는 옵션은 알파벳 두글자 이상으로 구성, 긴 옵션
```bash

## kubectl run 파드이름 --image=이미지이름 --port=포트번호
$ kubectl run nginx --image=nginx
```
