<template>
  <div class="controller">
    <div class="select">
      <label for="order"></label>
      <select
        name="order"
        id="order"
        class="selectbox"
        v-model="selected"
        v-on:change="sortTodo"
      >
        <option value="date-asc">Oldest</option>
        <option value="date-desc">Latest</option>
      </select>
    </div>
    <span class="clear" @:click="clearTodo">Clear All</span>
  </div>
</template>
<script>
export default {
  data() {
    return {
      selected: "date-asc",
    };
  },
  methods: {
    sortTodo() {
      this.$emit("sortItem", { value: this.selected });
    },
    clearTodo() {
      this.$emit("clearAll");
    },
  },
};
</script>
<style>
.controller {
  display: flex;
  justify-content: space-between;
}
.clear {
  cursor: pointer;
  font-size: 14px;
  font-weight: bold;
  color: rgb(171, 171, 171);
}
</style>
