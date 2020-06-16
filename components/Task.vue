<template>
  <li
    :class="{
      'item--active': !task.completed,
      'circle--active': !task.completed,
      'circle--completed': task.completed,
      'item--completed': task.completed
    }"
    class="item circle"
    tabindex="0"
    @click="toggleComplete(task)"
    @keydown.enter="toggleComplete(task)"
  >
    {{ task.title }}
  </li>
</template>

<script>
export default {
  name: 'Task',
  props: {
    task: {
      type: Object,
      required: true
    }
  },
  methods: {
    toggleComplete(task) {
      task.completed = !task.completed
    }
  }
}
</script>

<style scoped>
.item {
  position: relative;
  box-sizing: border-box;
  padding: 10px;
  margin-bottom: 10px;
  margin-left: 10px;
  margin-right: 10px;
  border: 0;
  border-radius: 20px;
  box-shadow: 0 0 1px rgb(36, 34, 34);
  color: #585353;
  background-color: #ffffff;
}

.item--completed {
  color: #d7dee6;
  text-decoration: line-through;
}

.circle::before {
  content: '';
  position: absolute;
  top: 8px;
  right: 13px;
  width: 22px;
  height: 22px;
  border-radius: 10px;
  box-shadow: 0 0 3px rgb(0, 0, 0);
}

.circle--active::before {
  background-color: #fff;
}

.circle--completed::before {
  content: '✓';
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #37d7b2;
  color: #fff;
}
</style>
