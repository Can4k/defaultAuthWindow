<template>
  <button @click="openAuth">ОТКРЫТЬ ОКНО</button>
  <auntification @closeWindow="isAuthWindowActive = false" :is-auth-window-active="isAuthWindowActive"/>
</template>

<script>
import Auntification from "@/components/authWindow/auntification";
export default {
  name: 'App',
  components: {
    Auntification
  },
  methods: {
    openAuth() {
      this.isAuthWindowActive = true;
    }
  },
  data() {
    return {
      isAuthWindowActive: false
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
