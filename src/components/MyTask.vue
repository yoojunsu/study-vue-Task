<template>
    <div class="task" :class="{ reminder: MyTask.reminder }" @dblclick="taskReminderToggle(MyTask.id)">
        <h3>
            {{ MyTask.text }}
            <i class="fas fa-times" @click="deleteTaskData(MyTask.id)"></i>
        </h3>
        <p>
            {{ MyTask.day }}
        </p>
    </div>
</template>

<script>
export default {
    name: "MyTask",
    props: {
        MyTask: String,
    },
    methods: {
        deleteTaskData(id) {
            this.emitter.emit('deleteDataShot',id);
        },
        taskReminderToggle(id) {
            console.log("ok");
            this.emitter.emit('reminderDataShot',id);
        }
    }
}
</script>

<style scoped>
.task {
background: #f4f4f4;
margin: 5px;
padding: 10px 20px;
cursor: pointer;
}

.task.reminder {
border-left: 5px solid green;
}

.task h3 {
display: flex;
align-items: center;
justify-content: space-between;
}

.fas {
    color: red;
}
</style>