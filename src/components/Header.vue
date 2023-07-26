<template>
  <header>
    <h1>
      {{ Title }}
    </h1>
    <Button :BtnText="(!AddTaskFormStatus) ? `Add Task` : `Close Task`" 
      :BtnBg="(!AddTaskFormStatus) ? `green` : `red`" 
      :AddTaskFormStatus="AddTaskFormStatus" 
    />
  </header>
</template>

<script>
import Button from "./Button.vue";

export default {
    name: "Header",
    props: {
      Title: String,
      AddTaskFormStatus: Boolean,
    },
    components: {
      Button,
    }
}
</script>

<style scoped>
    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
    }
</style>