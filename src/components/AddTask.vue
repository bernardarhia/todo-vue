<template>
  <form class="add-form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label>Task</label>
      <input v-model="text" type="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
        v-model="day"
        type="text"
        name="day"
        placeholder="Add Day & Time"
      />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input
        v-model="reminder"
        type="checkbox"
        name="reminder"
        placeholder="Add Task"
      />
    </div>
    <button class="btn btn-block">Add</button>
  </form>
</template>

<script>
export default {
  name: "AddTask",
  data() {
    return {
      text: "",
      day: "",
      reminder: false,
    };
  },
  methods: {
    onSubmit() {
      if (!this.text) {
        alert("Please add a task");
        return;
      }
      const { text, day, reminder, $emit } = this;
      const newTask = {
        id: Math.floor(Math.random() * 100000),
        text,
        day,
        reminder,
      };
      $emit("add-task", newTask);
      this.text = "";
      this.day = "";
      this.reminder = false;
    },
  },
};
</script>

<style scoped>
.add-form {
  margin-bottom: 3rem;
}
.form-control {
  margin: 20px 0;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
.btn-block {
  display: block;
  width: 100%;
}
</style>