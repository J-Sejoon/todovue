<template>
  <div class="inputBox shadow">
    <input
      type="text"
      placeholder="Type what you have to do"
      v-model="newTodoItem"
      v-on:keyup.enter="addTodo"
    />
    <span v-on:click="addTodo" class="addContainer">
      <i class="fa-solid fa-plus"></i>
    </span>

    <!-- 모달 팝업 설정 -->
    <AlertModal v-if="showModal">
      <h3 slot="header">경고</h3>
      <span slot="footer"
        >할 일을 입력해주세요
        <i
          class="closeModalBtn fa-regular fa-circle-xmark"
          v-on:click="showModal = false"
        ></i
      ></span>
    </AlertModal>
  </div>
</template>

<script>
import AlertModal from "./common/AlertModal.vue";

export default {
  data() {
    return {
      newTodoItem: "",
      showModal: false,
    };
  },
  methods: {
    addTodo() {
      //console.log("새로입력한 값은?", this.newTodoItem);
      //localStorage.setItem(this.newTodoItem, this.newTodoItem);
      //setItem(키,밸류)-로컬스토리지에 데이타를 추가하는 API

      //공백도 입력되는 상황을 막아주기 위해
      if (this.newTodoItem !== "") {
        let value = this.newTodoItem && this.newTodoItem.trim();
        //localStorage.setItem(value, value); 직접 저장하지 않게
        //this.newTodoItem = ""; //분리, 단일책임원칙
        this.$emit("addTodo", value); //상위 App.vuedp addTodo, value전달
        this.clearInput();
      } else {
        //텍스트 미 입력시 모달팝업
        this.showModal = true;
      }
    },
    clearInput() {
      //인풋박스 입력후 초기화
      this.newTodoItem = "";
    },
  },
  components: {
    AlertModal: AlertModal,
  },
};
</script>

<style scoped>
.inputBox {
  background: #ffb3b3;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
span.addContainer {
  float: right;
  background: linear-gradient(to right, #6677ff, #885bc7);
  width: 45px;
  border-radius: 0 5px 5px 0;
  cursor: pointer;
}
input {
  background: #ffb3b3;
  border: none;
  font-size: 1rem;
  text-align: center;
  width: calc(90% - 45px);
}
input:focus {
  outline: none;
}
i {
  color: white;
  vertical-align: middle;
}

.closeModalBtn {
  color: crimson;
}
</style>