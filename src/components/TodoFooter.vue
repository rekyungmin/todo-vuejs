<template>
  <v-row>
    <v-col>
      {{ activeLength }} items left
    </v-col>
    <v-col>
      <v-btn-toggle>
        <v-btn small @click="$emit('switchView', 'all')">All</v-btn>
        <v-btn small @click="$emit('switchView', 'active')">Active</v-btn>
        <v-btn small @click="$emit('switchView', 'completed')">Completed</v-btn>
      </v-btn-toggle>
    </v-col>
    <v-col>
      <v-btn
          small
          :class="{hidden: getVisibleClearButton}"
          @click="$emit('clearCompletedTodo')"
      >
        Clear Completed
      </v-btn>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: "TodoFooter",
  props: ["activeLength", "completedLength",],
  computed: {
    getVisibleClearButton() {
      return this.completedLength > 0 ? "" : "hidden";
    }
  }
}
</script>

<style scoped>
.hidden {
  visibility: hidden;
}
</style>