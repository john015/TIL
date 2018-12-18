## 색깔 참조 사이트

로딩중 svg 이미지

```
    [v-cloak]>* {
        display: none;
    }

    [v-cloak]::before {
        content: " ";
        display: block;
        position: absolute;
        width: 80px;
        height: 80px;
        background-image: url(./loading.svg);
        background-size: cover;
        left: 50%;
        margin-left: -40px;
        top: 50%;
        margin-top: -40px;
    }
```

## Vuex

        helper 함수  <methods>
    [vue]                [vuex]

동기 메소드(methods) > mutations
비동기 메소드(created) > actions

       helper 함수 <computed>
        data      >    state
     computed   >    getters

mutations
vue 에서 mutations 호출시 this.$store.commit('이름', 인자)

vuex 에서 state 호출시 state.[state 이름]

actions
vuex 에서 mutations 호출시 commit(뮤테이션이름,{파라미터})
vue components 에서 호출시 this.$store.dispatch
