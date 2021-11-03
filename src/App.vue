<template>
  <h1>TODO LIST</h1>
    <div class="input__block">
      <label for="input-task">Введите задачу </label><input v-model="inputTask" id="input-task" type="text">
      <button @click="addTask" id="btn-addtask">Добавить задачу</button>
    </div>
    <div class="radio__block">
      <h3>Приоритет задачи</h3>
      <input v-model="priority" id="high" type="radio" name="priority" checked value="red">
      <label for="high">Высокий</label>
      <input v-model="priority" id="medium" type="radio" name="priority" value="orange">
      <label for="medium">Средний</label>
      <input v-model="priority" id="low" type="radio" name="priority" value="blue">
      <label for="low">Низкий</label>
    </div>
    <h2>Список задач</h2>
    <div 
      class="task__list">
      <div
        v-for="task of todoList"
        :key="task.name" 
        :style="{ background: `${task.priority}`}"
        class="task__list-item">
        <p>{{ task.name }}</p>
        <button @click="deleteTask(task)">Удалить</button>
      </div>
    </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      inputTask: '',
      priority: '',
      todoList: [],
    }
  },

  methods: {
    addTask() {
      if (!this.inputTask) return true;

      const newTask = {
        name: this.inputTask,
        priority: this.priority
      };
      this.todoList.push(newTask);
      console.log(this.todoList);
      this.inputTask = '';
    },
    deleteTask(task) {
    const index = this.todoList.indexOf(task);
      if (index > -1) {
        this.todoList.splice(index, 1);
      }
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.radio__block label {
  color: #fff;
  border-radius: 5px;
  padding: 5px;
}

.radio__block label:nth-child(3) {
  background-color: red;
}

.radio__block label:nth-child(5) {
  background-color: orange;
}

.radio__block label:nth-child(7) {
  background-color: blue;
}

p {
  padding: 10px;
  margin: 0;
  min-width: 400px;
  text-align: start;
  color: #fff;
}

.task__list-item {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 5px auto;
  max-width: 500px;
  border-radius: 10px;
}

</style>
