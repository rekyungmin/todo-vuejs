<!--
이 컴포넌트 내부에서는 todo 아이템의 상태 변화에 대해서만 책임진다.
-->

<template>
  <li
      @mouseenter="todo.hasMousePointer=true"
      @mouseleave="todo.hasMousePointer=false"
  >
    <input
        type="checkbox"
        :checked="todo.isCompleted()"
        @click="todo.toggle()"
    >
    <label>{{ todo.value }}</label>
    <button
        v-if="todo.hasMousePointer"
        @click="$emit('removeItem', index)"
    >x
    </button>
  </li>
</template>

<script>
export default {
  name: "TodoListItem",
  props: ["todo", "index"],
}
</script>

<style scoped>

</style>