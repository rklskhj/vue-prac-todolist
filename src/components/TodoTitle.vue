<template>
  <div class="title">
    <div class="title__box">
      <p class="title__message">Good {{ message }},</p>
      <span
        v-on:keypress.enter="handleName"
        v-on:blur="handleBlur"
        class="title__name"
        ref="test"
        contenteditable="true"
      >
        {{ propName }}
      </span>
    </div>
    <p class="title__task">
      <span>오늘 해야 할 일은</span>
      <span class="title__task-total">
        <br />
        <em class="title__left">{{ propCount.left }}</em>
        /
        <em v-if="propCount.total" class="title__task-total">{{
          propCount.total
        }}</em>
        <em v-else class="title__task-total">0</em>
      </span>
      <br />
      <span>입니다!</span>
    </p>
  </div>
</template>
<script>
import getDate from "@/assets/commonJS/getDate";

export default {
  props: ["propCount", "propName"],
  data() {
    return {
      message: "",
    };
  },
  methods: {
    handleBlur(e) {
      const originalName = this.propName;
      const newName = e.target.innerText;
      if (newName !== originalName) {
        if (newName === "") {
          e.target.innerText = originalName;
        }
      } else {
        this.$emit("changeName", newName);
      }
    },
    handleName() {
      this.$refs.test.blur();
    },
  },
  mounted() {
    this.message = getDate().daytime;
  },
};
</script>
<style>
.title {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
.title__box {
  display: flex;
  gap: 15px;
}
.title__task {
  font-size: 1.5rem;
  font-weight: bold;
}
.title__task-total {
  font-size: 1.5rem;
  font-weight: bold;
  font-style: normal;
}
.title__left {
  font-size: 3rem;
  font-weight: bold;
  font-style: normal;
}
</style>
