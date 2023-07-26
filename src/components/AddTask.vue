<template>
<form class="add-form" @submit="newMyTaskPublish">
    <div class="form-control">
        <label>Task</label>
        <input 
            type="text" 
            name="text" 
            placeholder="Add Task" 
            v-model="AddTaskText"
        />
    </div>
    <div class="form-control">
        <label>Day & Time</label>
        <input
            type="text"
            name="day"
            placeholder="Add Day & Time"
            v-model="AddTaskDay"
        />
    </div>
    <div class="form-control form-control-check">
        <label>Set Reminder</label>
        <input type="checkbox" name="reminder" v-model="AddTaskReminder"/>
    </div>

    <input type="submit" value="Save Task" class="btn btn-block" />
</form>
</template>

<script>
export default {
    name: "AddTask",
    data() {
        return {
            AddTaskText: "",
            AddTaskDay: "",
            AddTaskReminder: false,
        }
    },
    methods: {
        newMyTaskPublish(e) {
            e.preventDefault();
            
            if(this.AddTaskText === "") {
                alert("뭐라도 작성해주세요");
                return
            }

            const newMyTask = {
                id: Math.floor(Math.random() * 10000),
                text: this.AddTaskText,
                day: this.AddTaskDay,
                reminder: this.AddTaskReminder,
            }

            this.emitter.emit('addNewMyTask',newMyTask);

            this.AddTaskText = '';
            this.AddTaskDay = '';
            this.AddTaskReminder = false;
        }
    }
}
</script>

<style>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>