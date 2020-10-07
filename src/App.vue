<template>
  <div id="app">
    <div>
      <h1>todos</h1>
      <input type="text" autofocus placeholder="What needs to be done?" v-model="newTodoValue" @keyup.enter="pushTodo">
      <div class="todo-list" v-for="(todo, index) in filteredTodoList" :key="index">
        <input class="todo-complete" type="checkbox" :checked="todo.state === 'completed'" @click="toggleStateTodo(index)">
        <label>{{ todo.value }} {{ todo.state }}</label>
        <button class="todo-delete" @click="popTodo(index)">x</button>
      </div>

      <div v-if="todoList.length">
        {{ todoList.length }} items left
        <button class="todo-view" @click="setViewState('all')">All</button>
        <button class="todo-view" @click="setViewState('active')">Active</button>
        <button class="todo-view" @click="setViewState('completed')">Completed</button>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {

  },
  data() {
    return {
      viewState: "all",
      todoList: [],
      newTodoValue: "",
    }
  },
  methods: {
    pushTodo() {
      if (this.newTodoValue === "") return;

      this.todoList.push({
        value: this.newTodoValue,
        state: "active",
      })
      this.newTodoValue = ""; // clear input
    },

    popTodo(index) {
      this.todoList.splice(index, 1);
    },

    toggleStateTodo(index) {
      this.todoList[index].state = this.todoList[index].state === "active" ? "completed" : "active";
    },

    setViewState(state) {
      this.viewState = state;
    }
  },
  computed: {
    filteredTodoList() {
      return this.todoList.filter(todo => this.viewState === "all" || todo.state === this.viewState);
    }
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
</style>
