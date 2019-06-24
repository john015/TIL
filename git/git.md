# git 기본

## \$ git init

- git 저장소 초기화 즉 생성됨
  지정된 폴더를 버전관리하겠다고 지정해주는 명렁어

## \$ git status

- 현재 git이 관리하고 있는 것에 대한 상태

## \$ git add

- 파일을 인식하고 버전관리를 시작함

## \$ git commit

- 변경한것들의 버전을 쓸수있음 --amend 쓰면 새로운 커밋을 추가 하지않고 기존 마지막 커밋을 수정함
  <br>
- \-a 수정 생성 한것들을 add 없이 바로 커밋할수있음<br>
- \-m "" 따로 텍스트에디터로 버전 쓰지않고 ""로 버전 쓸수있음 -am 가능

## \$ git log

- 역대 버전들을 볼수있음 <br>
- \--branches 모든 브렌치들의 로그를볼수있음 <br>
- \--graph 그래프로 보여줌 <br>
- \--decorate 시각화해줌 <br>
- \--oneline 한눈에 보게해줌 <br>

## \$ git log -p

- 역대 버전들의 변경점을 볼수있음

## \$ git diff

- commit 하기전 전버전과 다른점을 알려줌

## \$ git reset (log id값) --

- 입력한 id값의 상태로 되돌림

## git branch "새로운 브랜치 이름"

- 브렌치를 생성

## git checkout (-b) 전환할브렌치명

- 브렌치를 전환 <br>
- \-b 넣으면 브렌치를 생성하면서 전환할수있음

## git stash (apply)

- 진행중이던 내용을 커밋하지않고 헤드에 남겨놈<br>
- apply 까지넣으면 되돌림

## git stash pop

- 저장된 stash를 제거하고 불러옴

## git rm (파일)

- 실제 디렉토리에서 해당 파일을 삭제하고 staged함.
- git rm --cached를 하면 staged만 수행함.

## git reset --hard 로그주소

- \--hard 로그주소상태의 working directory(지금 진행중인 add commit 하지않는 상태) index (add만한상태) repository(커밋까지한 상태)
  를 다 돌림 <br>
- \--soft working directory만 빼고 index와 repository 를 해당로그상태로 돌림<br>
- \--mixed repository 만 해당로그상태로 돌림

## git merge (merge할 branch이름)

- 현재 brach를 기준으로 branch를 merge함.

## git remote add origin https://github.com/(username)/(repo name)

- 로컬에서 원격저장소 연결

## git remote (-v)

- 로컬저장소와 연결된 원격 저장소 확인 -v 는 상세보기 주소나옴

# Merge vs Rebase

## Merging 장점

- 이해하기 쉬움
- 원래 브랜치의 컨텍스트를 유지함.
- Fast-Forward Merge 를 하지 않는다면 브랜치 별로 커밋을 분리해 유지. 특히 이런 분리는 기능 브랜치에 유용.
- 원래 브랜치의 커밋들은 변경되지 않고 계속 유지되어 다른 개발자들의 작업과 공유되는 것에 대해 신경쓸 필요가 없음.

## Rebase 장점

- 단순한 히스토리
- 여러 개발자들이 같은 브랜치를 공유할 때 커밋을 합치는 가장 직관적이고 깔끔한 방법.

## Rebase 단점

- 충돌상황에서 다소 복잡. 커밋 순서대로 Rebase 를 하는데, 각 커밋마다 충돌해소를 순서대로 해주어야 한다. GUI를 사용할 경우 GUI프로그램이 가이드 해주지만, 역시 복잡한 것은 사실이다.
- push한 커밋들을 다른 사람이 pull 한 적이 있다면 히스토리가 꼬인다.

## Summary

- 여러 개발자들이 같은 브랜치를 공유할 때는 Rebase로 히스토리를 깔끔하게 유지하는데 좋다.
- 기능 브랜치를 합칠때는 Merge를 사용한다.
