<template>
  <div id="app">
    <div>
      <h1>todos</h1>
      <input type="text" autofocus placeholder="What needs to be done?" v-model="newTodoValue" @keyup.enter="pushTodo">
      <div class="todo-list" v-for="(todo, index) in filteredTodoList" :key="index">
        <input class="todo-complete" type="checkbox" :checked="todo.isCompleted()" @click="toggleState(todo)">
        <label>{{ todo.value }}</label>
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
      let value = (this.newTodoValue ?? "").trim();
      if (value.length === 0) return;

      this.todoList.push({
        value: value,
        state: "active",
        isCompleted() {
          return this.state === "completed";
        },
      })
      this.newTodoValue = "";
    },

    popTodo(index) {
      this.todoList.splice(index, 1);
    },

    toggleState(todo) {
      todo.state = todo.isCompleted() ? "active" : "completed";
    },

    setViewState(state) {
      this.viewState = state;
    },
  },
  computed: {
    filteredTodoList() {
      if (this.viewState === "all") return this.todoList;
      return this.todoList.filter(todo => todo.state === this.viewState);
    },
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
