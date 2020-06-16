<template>
  <div>
    <section class="tasks">
      <h2 class="title">All Tasks</h2>
      <ul class="list">
        <Task v-for="(task, index) in showed" :key="index" :task="task" />
      </ul>
      <input
        v-if="newTask"
        v-model="newTask.title"
        class="addTask"
        type="text"
        @keydown.enter="add"
        @blur="cancel"
      />
      <button v-if="!newTask" class="add" @click="onClick">+</button>
    </section>
    <ul class="filters">
      <li class="filter">
        <button @click="fetchAll">All</button>
      </li>
      <li class="filter">
        <button @click="fetchActive">
          Active
        </button>
      </li>
      <li class="filter">
        <button @click="fetchCompleted">
          Completed
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
import Task from '../components/Task'

export default {
  components: {
    Task
  },
  data() {
    return {
      newTask: null,
      tasks: [
        {
          title: 'Create New Project',
          completed: true
        },
        {
          title: 'Working Call',
          completed: false
        }
      ],
      showed: []
    }
  },
  created() {
    this.showed = this.tasks
  },
  methods: {
    onClick() {
      this.newTask = {
        title: '',
        completed: false
      }
    },
    add() {
      this.tasks.push(this.newTask)
      this.newTask = null
    },
    cancel() {
      this.newTask = null
    },
    fetchAll() {
      this.showed = this.tasks
    },
    fetchActive() {
      this.showed = this.tasks.filter((task) => !task.completed)
    },
    fetchCompleted() {
      this.showed = this.tasks.filter((task) => task.completed)
    }
  }
}
</script>

<style>
body {
  margin: 20px 0 0 20px;
  padding: 0;
  font-family: Roboto, serif;
  background-color: #f6f7fa;
}

button {
  padding: 15px;
  border: 0;
  border-radius: 10px;
  color: white;
  background-color: #17d6db;
}

.tasks {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 320px;
  background-color: #fff;
  border-radius: 40px;
}

.title {
  font-size: 18px;
  font-weight: normal;
}

.list {
  display: flex;
  flex-direction: column;
  width: 100%;
  margin: 0;
  padding: 0 0 70px;
  list-style: none;
}

.add {
  content: '+';
  position: absolute;
  left: calc(50% - 50px / 2);
  bottom: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50px;
  height: 50px;
  border: 0;
  border-radius: 100%;
  color: #fff;
  background-color: #5ca8e0;
  font-size: 40px;
  font-weight: 100;
}

.addTask {
  box-sizing: border-box;
  position: absolute;
  bottom: 20px;
  display: block;
  padding: 10px;
  width: 90%;
  border-radius: 20px;
}

.filters {
  display: flex;
  justify-content: space-around;
  width: 320px;
  padding: 10px 0;
  margin: 10px 0 0;
  border-radius: 10px;
  list-style: none;
  background-color: #fff;
}
</style>
