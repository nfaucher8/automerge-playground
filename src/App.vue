<script setup lang="ts">
import { Repo } from "@automerge/automerge-repo"
import HelloWorld from './components/HelloWorld.vue'
import {ref} from "vue";

export interface State {
  counter: number;
}

const repo = new Repo({ /* repo config */ })
const state = ref({ counter: 0 })

const handle = repo.create(state.value)

console.log(repo)
console.log(handle)

const add = () => {
  console.log("document change requested: Add")
  handle.change(document => {
    document.counter++;
    state.value = document;
  })
}
</script>
<template>
  <div>
    {{state}}
  </div>
  <HelloWorld msg="Vite + Vue" :add="add" :state="state" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
