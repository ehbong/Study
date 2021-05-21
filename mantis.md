# mantis

* [Docker를 사용한 빠른설치](https://hub.docker.com/r/vimagick/mantisbt)
```
  # 비밀번호 변경을 이메일로 전송이 아닌 관리자에게 권한을 주는 설정
  config_defaults_inc.php 파일수정
  $g_send_reset_password  = OFF 에 OFF 를 ON으로  수정
```
