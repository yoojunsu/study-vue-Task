<template>
  <button type="button" class="btn" :style="{ backgroundColor: BtnBg }" @click="addTaskformToggle">
    {{ BtnText }}
  </button>
</template>

<script>
export default {
    name: "Button",
    props: {
        BtnText: String,
        BtnBg: String,
        AddTaskFormStatus: Boolean,
    },
    methods: {
        addTaskformToggle() {
            this.emitter.emit('addTaskFormToggle');
        }
    }
}
</script>

<style>

</style>