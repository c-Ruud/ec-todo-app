<template>
  <div class="todo-items">
    <div class="todo-item">
      <input type="checkbox" @click="isChecked" :checkedItem="item.completed" />
      <div :class="{ completed: item.completed }">{{ item.title }}</div>
      <button @click="$emit('removedTodo', id)" class="remove-item">X</button>
    </div>
    <hr />
  </div>
</template>

<script>
export default {
  name: "todo-item",
  props: {
    item: Object,
  },
  methods: {
    isChecked() {
      this.$emit("checkedItem");
    },
  },
  emits: ["removedTodo", "checkedItem"],
};
</script>

<style scoped>
.todo-input {
  width: 100%;
  font-size: 18px;
  margin-bottom: 0.3rem;
}
.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 0.3rem;
  margin-bottom: 0.3rem;
  margin-left: 0.8rem;
  animation-duration: 0.09s;
}
.completed {
  text-decoration: line-through;
  color: rgba(214, 64, 126, 0.81);
}
.remove-item {
  cursor: pointer;
  margin-left: 14px;
  margin-right: 0.2rem;
  background-color: none;
  outline: none;
  border: none;
}
</style>
