<template>
  <div class="flex items-center my-3 gap-2">
    <div @click="toggle(id)" class="flex flex-1 items-center cursor-pointer">
      <img class="w-7" :src="isComplete ? tick : notTick" alt="Completion Status" />
      <p :class="['text-slate-700 ml-4 text-[17px] decoration-slate-500', { 'line-through': isComplete }]">
        {{ text }}
      </p>
    </div>
    <img @click="deleteTodo" :src="deleteIcon" alt="Delete" class="w-3.5 cursor-pointer" />
  </div>
</template>

<script>
import tick from '../assets/tick.png';
import notTick from '../assets/not_tick.png';
import deleteIcon from '../assets/delete.png';

export default {
  name: 'TodoItems',
  props: {
    text: String,
    id: Number,
    isComplete: Boolean
  },
  methods: {
    toggle() {
      this.$emit('toggle', this.id);
    },
    deleteTodo() {
      this.$emit('deleteTodo', this.id);
    }
  },
  data() {
    return {
      tick,
      notTick,
      deleteIcon
    };
  }
};
</script>

<style scoped>
/* Add any specific styles for TodoItems.vue here */
</style>