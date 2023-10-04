# Pycharm 환경설정

* [vscode key map 플러그인 소개](https://dubuholic.tistory.com/147)
* [추천 플러그인](https://vhxpffltm.tistory.com/m/184)
* [black 포메터 설정](https://pearlluck.tistory.com/743)
## git clone
* [파이참 gitclone](https://baessi.tistory.com/116)
* [파이참 설정 영상](https://opentutorials.org/course/3666/24539)

## venv 설정
* [파이참 venv 설정](https://sseambong.tistory.com/285)

## 단축키
```
F3 : 변수 또는 함수 tracking
Alt + Shift + R : 함수, 파일(모듈), 변수명 한꺼번에 변환하기.
Alt + Shift + X : 해당 코드 실행
Ctrl + G : 해당 변수, 파일, 함수가 사용된 코드 찾기.
Ctrl + L : 특정 번호의 Line으로 이동하기.
Ctrl + F : 현재 작업중인 파일 안에서 특정 문자열 검색 혹은 변환하기.
Ctrl + H : 프로젝트 전체를 대상으로 특정 문자열 검색 혹은 변환하기.
Shift 두번 : 프로젝트 전체에서 자신이 작업하고 싶은 파일 검색하여 열기.
Ctrl + Shift + F : 현재 커서가 놓여있는 파일의 코드 indentation 을 자동으로 정렬한다. (자동 코드 정리)

어떤 변수위에 커서를 두고
Ctrl + Alt + U : 해당 변수의 Dependency 를 한눈에 볼 수 있는 Class Diagram 을 표시한다.
파이썬 Console에서 바로 실행 (alt + shift + E)
Ctrl + Q : 해당 함수의 quick documentation을 볼 수 있다.

(커서가 메서드를 가리킬 때
Ctrl + Shift + Space : 매개 변수 정보
Ctrl + P : 현재 함수(혹은 메서드)의 파라미터 목록
F12 : 메서드 정의로 이동
Ctrl + w : 구역 설정
Alt + Shift + E : 커서 또는 선택된 영역 코드 실행 결과 보기
```

> python path를 인식 못할 때 경로 지정 방법
```bash
# path 확인
echo $PYTHONPATH
# path 지정
export PYTHONPATH=$PYTHONPATH:<경로: venv 사용 시 프로젝트경로/venv/lbi/python버전/site-packages >
```