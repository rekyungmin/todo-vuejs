<template>
  <v-app id="app">
    <h1 class="mb-10">todos</h1>
    <v-main>
      <v-container>
        <TodoList/>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import TodoList from "./components/TodoList.vue"

export default {
  name: "App",
  components: {
    TodoList,
  },
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
.container {
  min-width: 230px;
  max-width: 550px;
}
</style>
