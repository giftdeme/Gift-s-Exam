<template>
  <div class="bg-stone-900 grid py-4 min-h-screen">
    <Todo />
  </div>
</template>

<script>
import Todo from './components/Todo.vue';

export default {
  name: 'App',
  components: {
    Todo
  }
}
</script>

<style scoped>
/* Add any specific styles for App.vue here */
</style>