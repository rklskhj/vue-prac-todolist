<template>
  <div class="header">
    <h4 class="logo">My TodoList</h4>
    <p class="date">{{ timestamp }}</p>
  </div>
</template>
<script>
import getDate from "@/assets/commonJS/getDate";

export default {
  data() {
    return {
      timestamp: "",
    };
  },
  created() {
    this.timestamp = `${getDate().month}/${getDate().date} ${getDate().week}`;
  },
};
</script>
<style>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.logo {
}
</style>
