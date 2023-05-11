<template>
  <div>
    <TransitionGroup name="list" tag="ul">
      <li v-for="(todoItem, index) in propsdata" :key="index" class="shadow">
        <i class="checkBtn fa-regular fa-circle-check"></i>
        <span class="text">{{ todoItem }}</span>
        <span class="removeBtn" @click="removeTodo(todoItem, index)"
          ><i class="fa-solid fa-trash-can"></i
        ></span>
      </li>
    </TransitionGroup>
  </div>
</template>

<script>
export default {
  props: ["propsdata"],

  methods: {
    removeTodo: function (todoItem, index) {
      this.$emit("removeTodo", todoItem, index);
    },
  },
};
</script>

<style scoped>
ul {
  margin-top: 0;
  list-style: none;
  padding-left: 0;
}
li {
  display: flex;
  background: #c1dcff;
  height: 50px;
  line-height: 50px;
  margin: 10px 0;
  padding-left: 10px;
  border-radius: 5px;
  text-align: left;
}
.checkBtn {
  line-height: 50px;
  margin-right: 7px;
  color: deepskyblue;
}
.text {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.removeBtn {
  margin-left: auto;
  width: 40px;
  text-align: center;
  color: crimson;
  cursor: pointer;
}

.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
