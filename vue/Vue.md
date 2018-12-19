## 로딩중 svg 이미지

```javascript
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
