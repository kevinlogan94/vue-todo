<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Todo/>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Todo from "./components/Todo";

export default {
  name: 'app',
  components: {
    Todo
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
* {
  padding: 4px;
  margin: 8px;
}
input {
  cursor: pointer;
}
button {
  cursor: pointer;
}
.spacing-s { padding: 2px; }
.spacing-s--bottom { padding-bottom: 2px; }
.spacing-s-alt { margin: 2px; }
.spacing-s--bottom-alt { margin-bottom: 2px; }
</style>
