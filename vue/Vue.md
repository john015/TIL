
## Life cycle

**beforeCreate**

모든 훅 중에 가장 먼저 실행되는 훅이다. 아직 data와 events가 정의되지 않은 시점이므로 접근하려고 하면 에러가 난다.

**created**

이제 data와 events가 활성화되어 접근할 수 있다. 아직 DOM rendering이 안된상태다

**beforeMount**

DOM rendering이 일어나기 직전에 호출된다

**mounted**

DOM rendering이 일어난뒤 호출된다 dom에 접근이 가능하다 모든 하위 컴포넌트가 마운트된 상태를 보장하지는 않는다. 
ps. vm.$nextTick를 사용하면 전체가 렌더링된 상태를 보장할 수 있다. 

**beforeUpdate**

data가 변하여 data를 변경시키기 전에 실행된다. rerendering 전의 data를 얻을 수 있고 이 훅에서 data를 변경해도 rerendering은 실행되지 않는다.

**updated**

data가 변하여 rerendering이 일어난 후에 실행된다 여기서 상태를 변경하면 무한루프에 빠질 수 있다. mounted와 마찬가지로 모든 하위 컴포넌트가 업데이트된 상태를 보장하지는 않는다. 
ps. vm.$nextTick를 사용하면 전체가 렌더링된 상태를 보장할 수 있다. 

**beforeDestroy**

Destroy되기 직전에 호출된다

**destroyed**

Destroy된 후에 호출된다






# Vuex


## vue, vuex 비교
| vue          | vuex      |
| ------------ | --------- |
| methods      | mutations |
| created(비동기) | actions   |
| computed     | getters   |
| data         | state     |

## mutations
vue 에서 mutations 호출시 this.\$store.commit('이름', params)

## actions
vuex 에서 mutations 호출시 commit(mutationName,{params})
vue components 에서 호출시 this.\$store.dispatch
