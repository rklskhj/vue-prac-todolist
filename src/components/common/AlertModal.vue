<template>
  <div class="modal modal__dim" v-on:click.self="$emit('close')">
    <div class="modal__content">
      <p class="modal__text">
        <slot name="modal-text">(여기에 모달 내용이 들어가요!)</slot>
      </p>
      <button class="modal__close" v-on:click="$emit('close')">OK</button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {};
  },
};
</script>
<style>
.modal__dim {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  z-index: 999;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
}
.modal__content {
  display: flex;
  flex-direction: column;
  min-width: 25rem;
  margin: 0px auto;
  padding: 2rem;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 10px 30px -4px rgba(10, 10, 10, 0.2);
  transition: all 0.3s ease;
}
.modal__text {
  text-align: center;
  font-size: 1.4rem;
  color: #4a4a4a;
}
.modal__text::before {
  display: block;
  margin: 0 auto;
  text-align: center;
  line-height: 5rem;
  font-size: 2.2rem;
  font-weight: bold;
  content: "Oops !";
}
.modal__close {
  text-align: center;
  margin: 2.5rem auto 0;
  padding: 0.4rem 1rem;
  border: 1px solid #b1b1b1;
  border-radius: 0.2rem;
  font-size: 1.2rem;
  color: #555555;
}
.modal__close:hover {
  color: #323232;
  border-color: #4a4a4a;
}
</style>
