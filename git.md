# GIT, github

### 기본 강좌
* [깃허브 강좌 상](https://www.youtube.com/watch?v=FXDjmsiv8fI&t=38s)
* [깃허브 강좌 하](https://www.youtube.com/watch?v=GaKjTjwcKQo)
* [브랜치 종류 설명](https://mylko72.gitbooks.io/git/content/branch/branch_type.html)

### 기본 명령어
> 버전=커밋ID

>URL에는 원격저장소 뿐아니라 로컬저장소 경로도 포함될 수 있다.
```console
$ git init : 저장소 생성
$ git init --bare : 작업이 불가능하고 기능만 수행하는 저장소 생성(.git 내 파일만 존재)

$ git clone URL : 원격저장소에서 복제해서 저장소 생성
$ git clone --depth 숫자 URL : 최신 커밋을 숫자만큼만 복제해서 가져온다

$ git add 파일 : git이 파일을 추적하도록 명령, 새로 생성되거나 변경된것 등

$ git status : git 저장소의 상태를 확인

$ git commit
$ git commit -a : 추적중인 변경된 모든 파일을 add한다(한번도 add안된건 X)
$ git commit -m "메세지"
$ git commit --amend : 바로 이전 커밋을 수정한다. index의 변화없이 쓸 경우 커밋메세지만 수정되고, index가 변화했을 경우 반영되서 커밋된다.

$ git log : 커밋된 로그 조회
$ git log -p : 로그에서 출력되는 버전 간의 차이점을 출력하고 싶을 때

$ git diff 버전1..버전2 : 버전1과 버전2 간의 차이점을 비교할 때
$ git diff : git add하기 전(작업디렉터리)과 add한 후(index)의 파일 내용을 비교할 때

$ git reset --soft 버전 : 저장소만 이전 버전으로 돌아감
$ git reset --hard 버전 : 작업디렉터리까지 이전 버전으로 돌아감
$ git reset --hard ORIG_HEAD : 실수로 리셋을 한경우 이전으로 돌아감

$ git revert 버전 : 버전의 커밋을 취소한 내용을 새로운 버전으로 만드는 명령

$ git branch : branch 목록보기, *있는게 현재 브랜치
$ git branch 이름 : 이름으로 branch 생성

$ git checkout 브랜치명 : 현재 브랜치에서 브랜치명으로 이동
$ git checkout 버전 : 현재 브랜치에서 특정 버전으로 직접 이동

$ git branch -d 브랜치명 : 브랜치명 삭제
$ git branch -D 브랜치명 : 브랜치명 강제삭제
$ git branch -b 브랜치명 : 브랜치만들고 바로 checkout
$ git branch -m 브랜치명A 브랜치명B : 브랜치명을 A에서 B로 바꾼다

$ git log --branches(모든 브랜치를 보여준다) --decorate --graph(라인으로 표시) --oneline(커밋한줄로 표현)
$ git log 브랜치1..브랜치2 : 브랜치1에는 없고 브랜치2에는 있는 것을 비교해서 보여준다

$ git diff 브랜치1..브랜치2 : 브랜치간 차이점 비교

$ git merge B브랜치 : 현재 브랜치에서 B브랜치를 불러와서 병합한다.

$ git rebase B브랜치 : 현재 브랜치의 조상(base)을 B브랜치의 최신 커밋(rebase)으로 바꾸고, 파생된 커밋객체들과 B브랜치의 최신 커밋과 순서대로 병합해나간다. merge와 결과가 같지만 log에서 분기가 사라지고 일렬로 나온다.
$ git rebase --continue : rebase도중에 충돌이 났을 경우, 해결 후 마저 병합할때 쓴다.

$ git stash : 추적등록된(add 한번이상) 작업중인 변경사항들을 다른 곳에 저장해둔다.
$ git stash apply : 저장된 stash를 작업디렉터리에 불러온다
$ git stash list : 저장된 stash 리스트를 출력한다. {0}이 제일 최신, git reset을해도 stash 리스트는 지워지지 않는다.
$ git stash drop : {0} 최신 리스트 1개를 삭제한다.
$ git stash pop : apply하고 drop을 한다.

$ git reflog : HEAD의 변경이력(commit, reset 등)을 본다. {0}이 제일 최신

※ 원격저장소명엔 주로 오리지널(기본)이란 의미로 origin 를 많이 쓴다.

$ git remote : 원격저장소명을 출력
$ git remote -v : 원격저장소명과 URL을 출력
$ git remote add 원격저장소명 URL : 원격저장소 목록에 URL을 원격저장소명으로 저장한다. 이후부터는 원격저장소명만 쓰면 된다.
$ git remote remove 원격저장소명 : 원격저장소명을 삭제

$ git push -u 원격저장소명 브랜치명 (ex. git push -u origin master) : 원격저장소명이 가리키는 원격저장소로 최신 커밋상태를 업로드한다. -u 원격저장소명 브랜치명 를 쓰면, 로컬 브랜치와 원격 브랜치가 연결된다. 이후부터는 git push만 간단히 써도 push된다.
$ git push --tags : 로컬저장소의 태그들을 원격저장소로 업로드한다. github에서 releases탭이 활성화된다.

$ git pull : 원격저장소로부터 로컬저장소를 동기화하고 merge 한다

$ git fetch : 원격저장소로부터 로컬저장소를 동기화하지만 merge를 하지 않음
$ git fetch --prune : 원격 저장소에 더 이상 존재하지 않는 브랜치들에 해당하는 ref 들을 삭제

$ git log --branches --not --remotes : 푸쉬하지 않은 커밋의 수

$ git tag : 태그목록을 출력
$ git tag 태그명 : 현재 브랜치가 가리키는 커밋객체로 태그명을 갖는 태그를 만든다
$ git tag 태그명 브랜치명or버전: 브랜치가 가리키는 커밋객체 or 커밋ID로 태그명을 갖는 태그를 만든다 (light weight tag)
$ git tag -d 태그명 : 태그를 삭제한다
$ git tag -a 태그명 -m "메세지" : 주석을 달수 있는 태그를 만든다 (annotated tag)
$ git tag -v 태그명 : 태그의 자세한 정보(주석 포함)를 본다
```
[출처 빨간색코딩](https://sjh836.tistory.com/31)

### GIT TAG
* [Release tag 사용방법] (https://ios-development.tistory.com/356)

### GIT Action
* [git action 사용법](https://zzsza.github.io/development/2020/06/06/github-action/)


### GIT Page
* [git 정적 페이지 호스팅](https://eunche.github.io/deploy/github_static_web_page_hosting/)
