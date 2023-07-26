<template>
    <div v-for="(MyTask,i) in MyTasksData" :key="i">
        <MyTask :MyTask="MyTask" />
    </div>
</template>

<script>
import MyTask from "./MyTask.vue";
export default {
    name: "MyTasks",
    props: {
        MyTasksData: Array,
    },
    components: {
        MyTask,
    }
}
</script>

<style>

</style>