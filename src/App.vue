<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <user-list msg="Let's have more Vue!"/>
  </div>
</template>

<script>
import UserList from './components/UserList.vue'

export default {
  name: 'App',
  components: {
    UserList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
