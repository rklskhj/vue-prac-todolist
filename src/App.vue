<template>
  <div id="app">
    <div class="top">
      <TodoHeader />
      <TodoTitle v-bind:propsdata="checkCount" />
      <TodoInput v-on:addItem="addOneItem" />
    </div>
    <div class="bottom">
      <TodoController
        v-on:clearAll="clearAllItem"
        v-on:sortItem="sortAllItem"
      />
      <TodoList
        v-bind:propsdata="todoItems"
        v-on:removeItem="removeOneItem"
        v-on:toggleItem="toggleOneItem"
      />
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

import getDate from "./assets/commonJS/getDate";

export default {
  name: "App",
  components: {
    TodoHeader,
    TodoTitle,
    TodoInput,
    TodoController,
    TodoList,
    TodoFooter,
  },
  data() {
    return {
      todoItems: [],
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
  },
  methods: {
    addOneItem(todoItem) {
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
  },
  mounted() {
    this.sortTodoOldest();
  },
  created() {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
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
}
.bottom {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  background-color: gainsboro;
  padding: 30px 20px;
}
</style>
