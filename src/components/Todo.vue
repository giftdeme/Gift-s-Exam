<template>
  <div class="bg-white place-self-center w-11/12 max-w-md flex-col p-7 min-h-[550px] rounded-xl">
    <!-- Title Section -->
    <div class="flex items-center mt-7 gap-2">
      <img class="w-8" src="@/assets/todo_icon.png" alt="Todo Icon" />
      <h1 class="text-3xl font-semibold">To-Do List</h1>
    </div>

    <!-- Input Box Section -->
    <div class="flex item-center my-7 bg-gray-200 rounded-full">
      <input
        ref="inputRef"
        class="bg-transparent border-0 outline-none flex-1 h-14 pl-6 pr-2 placeholder:text-slate-600"
        type="text"
        placeholder="Add your task"
      />
      <button @click="add" class="border-none rounded-full bg-orange-600 w-32 h-14 text-white text-lg font-medium cursor-pointer">
        ADD +
      </button>
    </div>

    <!-- Todo List Section -->
    <div>
      <TodoItems
        v-for="item in todoList"
        :key="item.id"
        :text="item.text"
        :id="item.id"
        :isComplete="item.isComplete"
        @deleteTodo="deleteTodo"
        @toggle="toggle"
      />
    </div>
  </div>
</template>

<script>
import TodoItems from './TodoItems.vue';

export default {
  name: 'Todo',
  components: {
    TodoItems
  },
  data() {
    return {
      todoList: JSON.parse(localStorage.getItem("todos")) || []
    };
  },
  methods: {
    add() {
      const inputText = this.$refs.inputRef.value.trim();
      if (inputText === "") return;

      const newTodo = {
        id: Date.now(),
        text: inputText,
        isComplete: false
      };
      this.todoList.push(newTodo);
      this.$refs.inputRef.value = "";
    },
    deleteTodo(id) {
      this.todoList = this.todoList.filter(todo => todo.id !== id);
    },
    toggle(id) {
      this.todoList = this.todoList.map(todo => {
        if (todo.id === id) {
          return { ...todo, isComplete: !todo.isComplete };
        }
        return todo;
      });
    }
  },
  watch: {
    todoList: {
      handler() {
        localStorage.setItem("todos", JSON.stringify(this.todoList));
      },
      deep: true
    }
  }
};
</script>

<style scoped>
/* Add any styles specific to Todo component here */
</style>