<template>
  <div class="container">
    <Header Title="Task Tracker" :AddTaskFormStatus="AddTaskFormStatus" />
    <AddTask v-if="AddTaskFormStatus === true"/>
    <MyTasks :MyTasksData="MyTasksData"/>
  </div>
</template>

<script>
import Header from "./components/Header";
import MyTasks from "./components/MyTasks";
import AddTask from "./components/AddTask";
export default {
  name: "App",
  components: {
    Header,
    MyTasks,
    AddTask
  },
  data() {
    return {
      MyTasksData: [],
      AddTaskFormStatus: false,
    }
  },
  methods: {
    async fetchMyTasks() {
      const res = await fetch('http://localhost:5000/mytasks');
      const myTasksData = await res.json();

      return myTasksData;
    }
  },
  async created() {
    this.MyTasksData = await this.fetchMyTasks();
  },
  mounted() {
    this.emitter.on('deleteDataShot', (taskId) => {
      if(confirm('Are you sure?')) {
        this.MyTasksData = this.MyTasksData.filter( (targetMyTask) => {
          return targetMyTask.id !== taskId;
        });
      }
    });

    this.emitter.on('reminderDataShot', (taskId) => {
      console.log(taskId);
      this.MyTasksData = this.MyTasksData.map( (targetMyTask) => {
        if(targetMyTask.id === taskId) {
          return { ...targetMyTask, reminder: !targetMyTask.reminder};
        }

        return targetMyTask;
      });
    });

    this.emitter.on('addNewMyTask', (newTask) => {
      this.MyTasksData = [...this.MyTasksData, newTask];
      console.log(newTask);
    });

    this.emitter.on('addTaskFormToggle',() => {
      this.AddTaskFormStatus = !this.AddTaskFormStatus;
    });
  }

}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
