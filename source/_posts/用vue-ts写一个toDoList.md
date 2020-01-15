---
title: 用vue-ts写一个toDoList
date: 2020-01-14 16:45:09
categories:
- TS
tags:
- TS
---

1. app.vue

``` bash
<template>
  <div id="app">
    <newToDo @add="addNewItem" />
    <toDoList :list="list" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
// import HelloWorld from './components/HelloWorld.vue';
import newToDo from "./components/newToDo.vue";
import toDoList from "./components/toDoList.vue";

interface List {
  name: string;
  status: "done" | "todo" | "deleted";
}

@Component({
  components: {
    newToDo,
    toDoList
  },
  watch: {
    list(newValue: List) {
      localStorage.setItem("list", JSON.stringify(newValue));
    }
  }
})
export default class App extends Vue {
  list: Array<List> = localStorage.getItem("list")
    ? JSON.parse(<string>localStorage.getItem("list"))
    : [];
  addNewItem(value: string) {
    this.list.push({
      name: value,
      status: "todo"
    });
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: content-box;
}
</style>
```

2. newToDo.vue

``` bash
<template>
  <div>
    <input type="text" v-model="context" />
    <button @click="add">+</button>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({})
export default class newToDo extends Vue {
  context = "";
  add() {
    this.$emit("add", this.context);
    this.context = "";
  }
}
</script>
```

3. toDoList.vue

``` bash
<template>
  <div>
    <ul>
      <li v-for="(item,index) in list" :key="index">{{item}}</li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({
  props: {
    list: Array
  }
})
export default class toDoList extends Vue {}
</script>

<style lang="scss">
ul,
li {
  list-style: none;
}
</style>
```