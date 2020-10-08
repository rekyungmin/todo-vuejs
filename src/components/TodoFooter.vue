<template>
  <div>
    {{ activeLength }} items left
    <button @click="$emit('switchView', 'all')">All</button>
    <button @click="$emit('switchView', 'active')">Active</button>
    <button @click="$emit('switchView', 'completed')">Completed</button>
      <button v-if="completedLength > 0" @click="$emit('clearCompletedTodo')">Clear Completed</button>
  </div>
</template>

<script>
export default {
  name: "TodoFooter",
  props: ["activeLength", "completedLength",]
}
</script>

<style scoped>

</style>