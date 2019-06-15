# 프로세스 동기화

## Critical Section(임계영역)

- 동일한 자원을 동시에 접근하는 작업(e.g. 공유하는 변수 사용, 동일 파일을 사용하는 등)을 실행하는 코드 영역을 Critical Section 이라 칭한다.
- 임계영역을 수행하는 도중 인터럽트가 일어나면 의도치않은 결과가 일어날수있다.

### Critical Section Problem(임계영역 문제)

- 프로세스들이 Critical Section 을 함께 사용할 수 있는 프로토콜을 설계하는 것이다.

#### Requirements(해결을 위한 기본조건)

- Mutual Exclusion(상호 배제)
  프로세스 P1 이 Critical Section 에서 실행중이라면, 다른 프로세스들은 그들이 가진 Critical Section 에서 실행될 수 없다.
- Progress(진행)
  Critical Section 에서 실행중인 프로세스가 없고, 별도의 동작이 없는 프로세스들만 Critical Section 진입 후보로서 참여될 수 있다.
- Bounded Waiting(한정된 대기)
  P1 가 Critical Section 에 진입 신청 후 부터 받아들여질 때가지, 다른 프로세스들이 Critical Section 에 진입하는 횟수는 제한이 있어야 한다.

### 해결책

#### Lock

- 하드웨어 기반 해결책으로써, 동시에 공유 자원에 접근하는 것을 막기 위해 Critical Section 에 진입하는 프로세스는 Lock 을 획득하고 Critical Section 을 빠져나올 때, Lock 을 방출함으로써 동시에 접근이 되지 않도록 한다.

##### 한계

- 다중처리기 환경에서는 시간적인 효율성 측면에서 적용할 수 없다.

#### Semaphores(세마포)

- 소프트웨어상에서 Critical Section 문제를 해결하기 위한 동기화 도구

##### 종류

- OS는 Counting/Binary 세마포를 구분한다

###### 카운팅 세마포

- 가용한 개수를 가진 자원에 대한 접근 제어용으로 사용되며, 세마포는 그 가용한 자원의 개수 로 초기화 된다. 자원을 사용하면 세마포가 감소, 방출하면 세마포가 증가 한다.

###### 이진 세마포

- MUTEX 라고도 부르며, 상호배제의 (Mutual Exclusion)의 머릿글자를 따서 만들어졌다. 이름 그대로 0 과 1 사이의 값만 가능하며, 다중 프로세스들 사이의 Critical Section 문제를 해결하기 위해 사용한다.

##### 단점

- Busy Waiting(바쁜 대기)
  Critical Section 에 진입해야하는 프로세스는 진입 코드를 계속 반복 실행해야 하며, CPU 시간을 낭비하게 된다.
- Deadlock(교착상태)
  세마포가 Ready Queue 를 가지고 있고, 둘 이상의 프로세스가 Critical Section 진입을 무한정 기다리고 있고, Critical Section 에서 실행되는 프로세스는 진입 대기 중인 프로세스가 실행되야만 빠져나올 수 있는 상황을 지칭한다.

### 모니터

- 고급 언어의 설계 구조물로서, 개발자의 코드를 상호배제 하게끔 만든 추상화된 데이터 형태이다.
- 공유자원에 접근하기 위한 키 획득과 자원 사용 후 해제를 모두 처리한다. (세마포어는 직접 키 해제와 공유자원 접근 처리가 필요하다. )
