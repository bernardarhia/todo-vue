<template>
  <div class="container">
    <div class="wrapper">
      <Header title="Hello" />
      <Button
        :text="showAddTask ? 'Close' : 'Add Task'"
        :color="showAddTask ? 'blue' : 'red'"
        @btn-click="toggleShowTask"
      />
    </div>
    <div v-show="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <Tasks
      :tasks="tasks"
      @delete-task="deleteTask"
      @toggle-reminder="toggleReminder"
    />
  </div>
</template>

<script>
import Header from "./components/Header";
import Button from "./components/Button";
import Tasks from "./components/Tasks";
import AddTask from "./components/AddTask";
export default {
  name: "App",
  components: {
    Header,
    Button,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    };
  },
  methods: {
    addTask(task) {
      this.tasks = [...this.tasks, task];
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },
    toggleShowTask() {
      this.showAddTask = !this.showAddTask;
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: "Doctor's appointment",
        day: "March 13th at 1pm",
        reminder: true,
      },
      {
        id: 2,
        text: "Apple shopping",
        day: "February 12th at 3am",
        reminder: true,
      },
      {
        id: 3,
        text: "Meeting with client",
        day: "23rd October at 12pm",
        reminder: false,
      },
    ];
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Roboto:300,400,500,700");

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
body {
  font-family: "Roboto", sans-serif;
  font-size: 16px;
  color: #333;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid #254765;
  padding: 1rem;
}

.btn {
  display: inline-block;
  padding: 10px 20px;
  border: none;
  border-radius: 3px;
  background-color: #254765;
  color: #fff;
  cursor: pointer;
  transition: all 0.3s ease;
}
.wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 2rem;
}
</style>
