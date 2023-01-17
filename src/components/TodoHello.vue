<template>
  <div class="nameBox">
    <div class="hello">당신의 이름은 무엇입니까?</div>
    <label for="user-name"></label>
    <input
      type="text"
      id="user-name"
      placeholder="이름을 입력해주세요!"
      v-model="userName"
      v-on:keyup.enter="addUserName"
    />
  </div>
</template>
<script>
export default {
  data() {
    return {
      userName: "",
    };
  },
  methods: {
    addUserName() {
      this.$emit("addName", this.userName);
    },
  },
};
</script>
<style>
.nameBox {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 20px;
  text-align: center;
  font-size: 1.1rem;
  font-weight: bold;
  margin-top: 60px;
}
input[id="user-name"] {
  background: rgba(255, 255, 255, 0.154);
  border: none;
  color: white;
  height: 3rem;
  font-size: 1.3rem;
  text-align: center;
}
input::placeholder {
  color: white;
  text-decoration: underline;
  text-align: center;
}
</style>
