<template>
  <div>
    <TransitionGroup name="list" tag="ul">
      <!-- vue 2.2.0이상에서는 key값 필수 propsdata 로 바꿈-->
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
  /* App.vue로 이동
  data() {
    return { todoItems: [] }; //스토리지 내용을 집어넣을 빈배열
  },
  */
  /***************  App.vue로 이동
  created: function () {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  }, */
  methods: {
    removeTodo: function (todoItem, index) {
      //console.log("키: " + index + ", 밸류:" + todoItem);
      this.$emit("removeTodo", todoItem, index);

      /* App.vue로 가져감
      localStorage.removeItem(todoItem); //로컬스토리지에서 삭제
      this.todoItems.splice(index, 1); */
      //.splice() -배열 특정 항목을 제거
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
  text-overflow: ellipsis; /*말줄임표 적용*/
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