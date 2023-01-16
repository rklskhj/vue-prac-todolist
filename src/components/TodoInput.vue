<template>
  <div class="add">
    <input
      type="text"
      class="add__input"
      placeholder="Enter your task"
      v-model="newTodoItem"
      v-on:keyup.enter="addTodoItem"
    />
    <span @:click="addTodoItem" class="add__button">👉</span>
  </div>
</template>
<script>
export default {
  data() {
    return {
      newTodoItem: "",
    };
  },
  methods: {
    addTodoItem() {
      if (this.newTodoItem !== "") {
        this.$emit("addItem", this.newTodoItem);
        this.clearInput();
      } else {
        window.alert("빈칸을 채워주세요!");
      }
    },
    clearInput() {
      this.newTodoItem = "";
    },
  },
};
</script>
<style>
.add {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 3rem;
  background-color: rgba(240, 248, 255, 0.332);
  border-radius: 2rem;
  box-shadow: 5px 5px 20px rgba(0, 0, 0, 0.423);
}
.add__input {
  width: 80%;
  height: 2.5rem;
  margin-right: 40px;
  margin-left: 20px;
  border: 0 solid black;
  background-color: rgba(255, 255, 255, 0);
  font-size: 1.2rem;
}
input:focus {
  outline: none;
}
.add__button {
  display: flex;
  justify-content: center;
  text-align: center;
  line-height: 2.2rem;

  width: 2.5rem;
  height: 2.5rem;
  border-radius: 50%;
  background-color: #f3e6e6;

  font-size: 1.5rem;
  cursor: pointer;
}
</style>
