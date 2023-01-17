<template>
  <div id="app">
    <AlertModal v-show="modalVisible" v-on:close="modalVisible = false">
      <template v-slot:modal-text>중복되는 할 일이 있어요!</template>
    </AlertModal>
    <div class="top" v-if="userName">
      <TodoHeader />
      <TodoTitle
        v-bind:propCount="checkCount"
        v-bind:propName="userName"
        v-on:changeName="addUserName"
      />
      <TodoInput v-on:addItem="addOneItem" v-on:alertModal="showModal" />
    </div>
    <div class="iftop" v-else>
      <TodoHeader />
      <TodoHello v-on:addName="addUserName" />
    </div>
    <div class="bottom" v-if="userName">
      <TodoController
        v-on:clearAll="clearAllItem"
        v-on:sortItem="sortAllItem"
      />
      <TodoList
        v-bind:propEmpty="isEmpty"
        v-bind:propItems="todoItems"
        v-on:removeItem="removeOneItem"
        v-on:toggleItem="toggleOneItem"
      />
      <TodoFooter />
    </div>
    <div class="ifbottom" v-else>
      <TodoController
        v-on:clearAll="clearAllItem"
        v-on:sortItem="sortAllItem"
      />
      <TodoList />
      <TodoFooter />
    </div>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoTitle from "./components/TodoTitle.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoController from "./components/TodoController.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";
import TodoHello from "./components/TodoHello.vue";

import getDate from "./assets/commonJS/getDate";
import AlertModal from "./components/common/AlertModal.vue";

export default {
  name: "App",
  components: {
    TodoHeader,
    TodoHello,
    TodoTitle,
    TodoInput,
    TodoController,
    TodoList,
    TodoFooter,
    AlertModal,
  },
  data() {
    return {
      modalVisible: false,
      modalText: "",
      todoItems: [],
      userName: "",
    };
  },
  computed: {
    checkCount() {
      const checkleftItem = () => {
        let leftCount = 0;
        for (let i = 0; i < this.todoItems.length; i++) {
          if (this.todoItems[i].completed === false) {
            leftCount++;
          }
        }
        return leftCount;
      };

      const count = {
        total: this.todoItems.length,
        left: checkleftItem(),
      };
      return count;
    },
    isEmpty() {
      return this.todoItems.length <= 0 ? true : false;
    },
  },
  methods: {
    addOneItem(todoItem) {
      // 빈 내용인 경우
      if (todoItem === "") {
        this.modalVisible = !this.modalVisible;
        this.modalText = "the form is empty. Please enter your task";
        return false;
      }
      // 중복되는 내용인 경우
      for (let i = 0; i < this.todoItems.length; i++) {
        if (this.todoItems[i].item === todoItem) {
          this.modalVisible = !this.modalVisible;
          this.modalText = "I think you've already had the task";
          return false;
        }
      }
      // 저장할 정보
      const value = {
        item: todoItem,
        date: `${getDate().date} ${getDate().week}`,
        time: getDate().time,
        completed: false,
      };
      localStorage.setItem(todoItem, JSON.stringify(value));
      this.todoItems.push(value);
    },
    toggleOneItem(todoItem) {
      todoItem.completed = !todoItem.completed;
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    removeOneItem(todoItem, index) {
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
    },
    clearAllItem() {
      this.todoItems = [];
      localStorage.clear();
    },
    sortTodoLatest() {
      this.todoItems.sort(function (a, b) {
        return b.time - a.titme;
      });
    },
    sortTodoOldest() {
      this.todoItems.sort(function (a, b) {
        return a.time - b.time;
      });
    },
    sortAllItem(selectedSort) {
      if (selectedSort.value === "date-desc") {
        this.sortTodoLatest();
      } else if (selectedSort.value === "date-asc") {
        this.sortTodoOldest();
      }
    },
    addUserName(userName) {
      localStorage.setItem("userName", userName);
      this.userName = userName;
    },
    showModal(text) {
      this.modalText = text;
      this.modalVisible = !this.modalVisible;
    },
  },
  mounted() {
    this.sortTodoOldest();
  },
  created() {
    this.userName = localStorage.getItem("userName");

    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== "userName") {
          this.todoItems.push(
            JSON.parse(localStorage.getItem(localStorage.key(i)))
          );
        }
      }
    }
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
#app {
}
.top {
  display: flex;
  flex-direction: column;
  gap: 3rem;
  background: linear-gradient(160deg, #3670cb, #c58bc0);
  color: white;
  padding: 20px 20px;
  height: 25rem;
}
.iftop {
  display: flex;
  flex-direction: column;
  gap: 3rem;
  background: linear-gradient(160deg, #3670cb, #c58bc0);
  color: white;
  padding: 20px 20px;
  height: 25rem;
}
.bottom {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  background-color: gainsboro;
  padding: 30px 20px;
  height: 24.813rem;
}
.ifbottom {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  background-color: gainsboro;
  padding: 30px 20px;
  height: 24.813rem;
}
</style>
