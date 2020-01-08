<template>
  <div class="board-container">
    <h3>TODO-LIST</h3>
    <div class="input-task-container">
      <input class="input-task-name" v-model="inputTaskName" />
      <button class="add-btn" @click="addTask">Add</button>
    </div>
    <div class="task-list-container">
      <ul>
        <li class="task-list-item" v-for="(task,index) in taskList" :key="task.name">
          <input v-model="task.isCheck" type="checkbox" />
          <span :class="{'is-check': task.isCheck}">{{task.name}}</span>
          <button class="delete-task-btn" @click="deleteTask(index)">DELETE</button>
        </li>
        <li class="clear-container">
          <button @click="clearTask" class="clear-btn">CLEAR</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Board",

  data() {
    return {
      inputTaskName: "",
      taskList: [{ name: "asdf", isCheck: false }]
    };
  },
  methods: {
    addTask() {
      const { inputTaskName } = this;
      this.taskList.push({ name: inputTaskName, isCheck: false });
      this.inputTaskName = "";
    },
    deleteTask(taskIndex) {
      if (taskIndex > -1) {
        this.taskList.splice(taskIndex, 1);
      }
    },
    clearTask() {
      this.taskList = [];
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.board-container {
  max-width: 400px;
  margin: auto;
}
.task-list-item {
  border: 1px solid black;
  display: flex;
  justify-content: center;
  align-items: center;
}
.input-task-name {
  height: 50px;
  border: none;
  font-size: 30px;
  width: 400px;
}
.add-btn,
.delete-task-btn {
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}
.input-task-container {
  position: relative;
}
.task-list-container {
  position: relative;
  height: 400px;
  background-color: white;
}
.clear-container {
  text-align: right;
  position: absolute;
  width: 100%;
  bottom: 0;
}
ul {
  padding: 0;
  list-style: none;
}
li {
  min-height: 40px;
  position: relative;
}
button {
  color: skyblue;
  border: none;
  font-size: 18px;
}
.clear-btn {
  margin: auto 16px;
}
.is-check {
  color: red;
  text-decoration: line-through;
}
</style>
