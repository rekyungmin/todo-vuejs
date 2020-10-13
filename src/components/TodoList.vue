<!--
이 컴포넌트 내부에서는 todos array에 대한 모든 책임을 가진다.
-->

<template>
  <div>
    <v-text-field
        outlined
        autofocus
        placeholder="What needs to be done?"
        v-model="newTodoValue"
        @keyup.enter="pushTodo"
    />
    <div :class="{outline: this.todos.length}">
      <TodoListItem
          v-for="(todo, index) in viewTodos"
          :key="index"
          :index="index"
          :todo="todo"
          @removeItem="popTodo"/>
    </div>
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


class TodoData {
  constructor(id, value) {
    this.id = id;
    this.value = value;
    this.isCompletedState = false
    this.hasMousePointer = false;
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
      return this.todos.filter(todo => !todo.isCompletedState);
    },
    completedTodos() {
      return this.todos.filter(todo => todo.isCompletedState);
    },
  },
  methods: {
    pushTodo() {
      const value = (this.newTodoValue ?? "").trim();
      if (value.length === 0) return;
      this.todos.push(new TodoData(this.todos.slice(-1).id + 1, value));
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
.outline {
  border: 1px rgba(0, 0, 0, 0.12) solid;
}
</style>