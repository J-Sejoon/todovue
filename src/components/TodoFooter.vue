<template>
  <div class="clearAllContainer">
    <span v-on:click="clearTodo" class="clearAllBtn">Clear All</span>
  </div>
</template>

<script>
export default {
  methods: {
    clearTodo() {
      this.$emit("removeAll");
    },
  },
};
</script>

<style scoped>
.clearAllContainer {
  background: white;
  border-radius: 5px;
  line-height: 50px;
  width: 120px;
  margin: 0 auto;
  cursor: pointer;
}
.clearAllBtn {
  color: crimson;
  display: block;
}
</style>