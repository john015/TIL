# cli 기본 & git 기본

## \$ cat f1.txt

-> f1.txt 파일을 읽는 명령어

## \$ cp f1.txt(복사할파일) f2.txt(복사될파일명)

-> 파일을 복사함

## \$ git

-> git이 잘 설치되었는지 알아보는 명령어

## \$ git init

-> git 저장소 초기화 즉 생성됨
지정된 폴더를 버전관리하겠다고 지정해주는 명렁어

## \$ git status

-> 현재 git이 관리하고 있는 것에 대한 상태

## \$ git add

-> 파일을 인식하고 버전관리를 시작함

## \$ git commit

-> 변경한것들의 버전을 쓸수있음 --amend 쓰면 커밋 버전 바꿀수있음
<br>
-a 수정 생성 한것들을 add 없이 바로 커밋할수있음<br>
-m "" 따로 텍스트에디터로 버전 쓰지않고 ""로 버전 쓸수있음 -am 가능

## \$ git log

-> 역대 버전들을 볼수있음 <br>
--branches 모든 브렌치들의 로그를볼수있음 <br>
--graph 그래프로 보여줌 <br>
--decorate 시각화해줌 <br>
--oneline 한눈에 보게해줌 <br>

## \$ git log -p

-> 역대 버전들의 변경점을 볼수있음

## \$ git diff

-> commit 하기전 전버전과 다른점을 알려줌

## \$ git reset (log id값) --

-> 복붙한 log 값상태로 되돌림

# 브렌치 관련

## git branch "새로운 브랜치 이름"

-> 브렌치를 생성

## git checkout (-b) 전환할브렌치명

->브렌치를 전환 <br>
b 넣으면 브렌치를 생성하면서 전환할수있음

## git log -p 브렌치1..브렌치2

->브렌치1에는 없고 브렌치2에는 없는 커밋을 보여줌<br>
-p 를붙이면 소스코드까지 볼수있음

## git diff 브랜치1..브렌치

->브렌치1에는 없고 브렌치2에는 없는 소스코드을 비교해줌

## git stash (apply)

->진행중이던 내용을 커밋하지않고 헤드에 남겨놈<br>
어플라이 까지넣으면 되돌림

## git stash pop

->저장된 스테쉬를 제거하고 불러옴

## git reset --hard 로그주소

--hard 로그주소상태의 working directory(지금 진행중인 add commit 하지않는 상태) index (add만한상태) repository(커밋까지한 상태)
를 다 돌림 <br>
--soft working directory만 빼고 index와 repository 를 해당로그상태로 돌림<br>
--mixed repository 만 해당로그상태로 돌림

# github(원격저장소)

## git init --bare (저장소이름)

->원격저장소 만듬

## git push

->로컬저장소에서 변경된걸 원격 저장소로 옮김

## git clone https://github.com/git/git.git(깃원격저장소주소) (복제될 디렉토리이름)

->로컬저장소로 원격저장소를 불러옴

## git remote add origin https://github.com/git/git.git(깃원격저장소주소)

-->로컬저장소에 원격저장소 연결

## git remote (-v)

-->로컬저장소와 연결된 원격 저장소 확인 -v 는 상세보기 주소나옴

## git push -u origin master

-->원격저장소에 연결 마스터브랜치를 푸쉬하다 -u는 처음만 쓰면됨 로컬브랜치와 원격브랜치를 동기화 > 담부터는 git push만 하면 자동으로 올려줌
