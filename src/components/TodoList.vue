<!--
이 컴포넌트 내부에서는 todos array에 대한 모든 책임을 가진다.
-->

<template>
  <div>
    <div>
      <input
          type="text"
          placeholder="What needs to be done?"
          autofocus
          v-model="newTodoValue"
          @keyup.enter="pushTodo"
      >
    </div>
    <TodoListItem
        v-for="(todo, index) in viewTodos"
        :key="index"
        :index="index"
        :todo="todo"
        @removeItem="popTodo"
    />
    <TodoFooter
        v-if="todos.length"
        :activeLength="activeTodos.length"
        :completedLength="completedTodos.length"
        @switchView="setViewState"
        @clearCompletedTodo="clearCompleted"
    />
  </div>
</template>

<script>
import TodoListItem from "@/components/TodoListItem";
import TodoFooter from "@/components/TodoFooter";

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
  name: "TodoList",
  components: {
    TodoListItem,
    TodoFooter,
  },
  data() {
    return {
      viewState: "all",
      todos: [],
      newTodoValue: "",
    }
  },
  computed: {
    viewTodos() {
      if (this.viewState === "all") return this.todos;
      else if (this.viewState === "active") return this.activeTodos;
      else return this.completedTodos;
    },
    activeTodos() {
      return this.todos.filter(todo => todo.state === "active");
    },
    completedTodos() {
      return this.todos.filter(todo => todo.state === "completed");
    },
  },
  methods: {
    pushTodo() {
      let value = (this.newTodoValue ?? "").trim();
      if (value.length === 0) return;
      this.todos.push(new Todo(value));
      this.newTodoValue = "";
    },
    popTodo(index) {
      this.todos.splice(index, 1);
    },
    setViewState(state) {
      this.viewState = state;
    },
    clearCompleted() {
      this.todos = this.activeTodos;
    }
  },
}
</script>

<style scoped>

</style>