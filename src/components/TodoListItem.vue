<!--
이 컴포넌트 내부에서는 todo 아이템의 상태 변화에 대해서만 책임진다.
-->

<template>
  <div
      @mouseenter="todo.hasMousePointer=true"
      @mouseleave="todo.hasMousePointer=false"
  >
    <v-list-item>
      <v-checkbox
          v-model="todo.isCompletedState"
      />
      <label
          :class="{'todo-completed': todo.isCompletedState}"
      >
        {{ todo.value }}
      </label>
      <v-spacer/>
      <v-icon
          medium
          v-if="todo.hasMousePointer"
          @click="$emit('removeItem', index)"
      >
        mdi-alpha-x-circle
      </v-icon>
    </v-list-item>
    <v-divider/>
  </div>
</template>

<script>
export default {
  name: "TodoListItem",
  props: ["todo", "index"],
}
</script>

<style scoped>
.todo-completed {
  text-decoration: line-through;
  color:#d9d9d9;
}
</style>