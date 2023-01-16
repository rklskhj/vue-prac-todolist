<template>
  <div class="title">
    <p class="title__message">{{ message }}</p>
    <p class="title__task">
      <span>오늘 해야 할 일은</span>
      <span class="title__task-total">
        <br />
        <em class="title__left">{{ propsdata.left }}</em>
        /
        <em v-if="propsdata.total" class="title__task-total">{{
          propsdata.total
        }}</em>
      </span>
      <br />
      <span>입니다!</span>
    </p>
  </div>
</template>
<script>
export default {
  props: ["propsdata"],
  data() {
    return {
      message: "반가워, 긍정!",
    };
  },
};
</script>
<style>
.title {
  display: flex;
  flex-direction: column;
  gap: 1rem;
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
