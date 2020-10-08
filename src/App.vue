<template>
  <div id="app">
    <div>
      <h1>todos</h1>
      <div>
        <input
            type="text"
            placeholder="What needs to be done?"
            autofocus
            v-model="newTodoValue"
            @keyup.enter="pushTodo"
        >
      </div>

      <div
          v-for="(todo, index) in viewTodos"
          :key="index"
          @mouseenter="todo.hasMousePointer=true"
          @mouseleave="todo.hasMousePointer=false"
      >
        <input
            type="checkbox"
            :checked="todo.isCompleted()"
            @click="todo.toggle()"
        >
        <label>{{ todo.value }}</label>
        <button v-if="todo.hasMousePointer" @click="popTodo(index)">x</button>
      </div>

      <div v-if="todoList.length">
        {{ todoList.length }} items left
        <button @click="setViewState('all')">All</button>
        <button @click="setViewState('active')">Active</button>
        <button @click="setViewState('completed')">Completed</button>
        <button v-if="completedTodos.length > 0" @click="clearCompleted">Clear Completed</button>

      </div>
    </div>
  </div>
</template>

<script>

class Todo {
  constructor(value, state="active") {
    this.value = value;
    this.state = state;
    this.hasMousePointer = false;
  }
  isCompleted() {
    return this.state === "completed";
  }
  toggle() {
    this.state = this.isCompleted() ? "active" : "completed";
  }
}

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

  computed: {
    viewTodos() {
      if (this.viewState === "all") return this.todoList;
      else if (this.viewState === "active") return this.activeTodos;
      else return this.completedTodos;
    },
    activeTodos() {
      return this.todoList.filter(todo => todo.state === "active");
    },
    completedTodos() {
      return this.todoList.filter(todo => todo.state === "completed");
    },
  },

  methods: {
    pushTodo() {
      let value = (this.newTodoValue ?? "").trim();
      if (value.length === 0) return;
      this.todoList.push(new Todo(value));
      this.newTodoValue = "";
    },

    popTodo(index) {
      this.todoList.splice(index, 1);
    },

    setViewState(state) {
      this.viewState = state;
    },

    clearCompleted() {
      this.todoList = this.activeTodos;
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
