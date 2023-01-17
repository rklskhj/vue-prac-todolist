<template>
  <ul class="list" v-bind:class="listempty">
    <li
      class="list__item"
      v-for="(todoItem, index) in propItems"
      :key="todoItem"
    >
      <div class="list__box">
        <input
          type="checkbox"
          :id="todoItem.item"
          :checked="todoItem.completed === true"
          v-on:change="toggleComplete(todoItem)"
        />
        <label :for="todoItem.item" class="list__label">
          <p v-if="todoItem.completed === true" class="list__text-done">
            {{ todoItem.item }}
          </p>
          <p v-else-if="todoItem.completed === false" class="list__text">
            {{ todoItem.item }}
          </p>
        </label>
      </div>
      <div class="delete__box">
        <span class="list__delete" @:click="removeTodo(todoItem, index)"
          >X</span
        >
        <p class="list__date">{{ todoItem.date }}</p>
      </div>
    </li>
  </ul>
</template>
<script>
export default {
  props: ["propItems", "propEmpty"],
  computed: {
    listempty() {
      return this.propEmpty ? "list--empty" : null;
    },
  },
  methods: {
    toggleComplete(todoItem) {
      this.$emit("toggleItem", todoItem);
    },
    removeTodo(todoItem, index) {
      this.$emit("removeItem", todoItem, index);
    },
  },
};
</script>
<style>
.list {
  display: flex;
  flex-direction: column;
  gap: 20px;
  list-style: none;
}
.list__item {
  display: flex;
  justify-content: space-between;

  width: 100%;
  height: 3rem;
  padding: 0px 15px;
  background-color: rgb(243, 243, 243);
}
.list__box {
  display: flex;
  align-items: center;
  gap: 10px;

  font-weight: bold;
}
.delete__box {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  justify-content: center;
  gap: 6px;
  font-size: small;
  color: rgb(171, 171, 171);
}
.list__delete {
  cursor: pointer;
}
.list__date {
  font-weight: bold;
}
.list__text-done {
  text-decoration: line-through;
}
input[type="checkbox"] {
  position: relative;
  top: 1.5px;
  transform: scale(1.5);
}
</style>
