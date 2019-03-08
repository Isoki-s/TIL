App.vueに<transition>を追加。

```App.vue
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">TOP</router-link> | 
      <router-link to="/starwars">starwars</router-link>
    </div>
    <transition mode="out-in"> <!-- 追加 -->
      <router-view/>
    </transition> <!-- 追加 -->
  </div>
</template>
```

cssに追記

#### 普通

```app.css
.v-enter-active, .v-leave-active {
  transition: opacity .5s;
}
.v-enter, .v-leave-to {
  opacity: 0;
}

```

#### 左から何かが来てる。わたしはそれを右に受け流ぅぅぅぅぅぅ

```
.v-enter {
  transform: translate(-100px, 0);
  opacity: 0;
}
.v-enter-to {
  opacity: 1;
}
.v-enter-active {
  transition: all 1s 0s ease;
}
.v-leave {
  transform: translate(0, 0);
  opacity: 1;
}
.v-leave-to {
  transform: translate(100px, 0);
  opacity: 0;
}
.v-leave-active {
  transition: all .5s 0s ease;
}
```

#### 左から何かが来てる。わたしはそれを左に押し返すぅぅぅぅぅぅ

```
.v-enter {
  transform: translate(-100px, 0);
  opacity: 0;
}
.v-enter-to {
  opacity: 1;
}
.v-enter-active {
  transition: all 1s 0s ease;
}
.v-leave {
  transform: translate(0, 0);
  opacity: 1;
}
.v-leave-to {
  transform: translate(100px, 0);
  opacity: 0;
}
.v-leave-active {
  transition: all .5s 0s ease;
}
```
