# Git-flow

## repository 구성

- Repository는 Upstream Remote Repository, Origin Remote Repository, Local Repository 이렇게 세 부분으로 구성되어있다.
- Upstream Repository는 개발자들이 공유하는 저장소로 최신 소스코드가 저장되어 있는 원격 저장소이다.
- Origin Repository는 Upstream Repository를 Fork한 원격 개인 저장소이다.
- Local Repository는 내 컴퓨터에 저장되어 있는 개인 저장소이다.

<img src="https://user-images.githubusercontent.com/32455422/60097854-437e9f00-978f-11e9-9250-5e520cbbc240.png">

위 그림은 Git Repository 구성과 워크플로우를 설명하고 있다. Local Repository에서 작업을 완료한 한 후 작업 브랜치을 Origin Repository에 push합니다. 그리고 Github에서 Origin Repository에 push한 브랜치를 Upstream Repository로 merge하는 Pull Request를 생성하고 코드리뷰를 거친 후 merge 합니다. 다시 새로운 작업을 할 때 Local Repository에서 Upstream Repository를 pull 한다.

## branch 구성

Git-flow에는 5가지 종류의 브랜치가 존재한다. 항상 유지되는 메인 브랜치들(master, develop)과 일정 기간 동안만 유지되는 보조 브랜치들(feature, release, hotfix)가 있다.

- master : 제품으로 출시될 수 있는 브랜치
- develop : 다음 출시 버전을 개발하는 브랜치
- feature : 기능을 개발하는 브랜치
- release : 이번 출시 버전을 준비하는 브랜치
- hotfix : 출시 버전에서 발생한 버그를 수정 하는 브랜치

## Summary

![git-flow_overall_graph](https://user-images.githubusercontent.com/32455422/60098246-05ce4600-9790-11e9-8e49-718fce27367b.png)
