<template>
  <div class="todo-items">
    <div class="todo-item">
      <input type="checkbox" v-model="completed" v-on:input="checkTodo" />
      <div :class="{ completed: completed }">{{ title }}</div>
      <button class="remove-item" @click="removeTodo(index)">X</button>
    </div>
    <hr />
  </div>
</template>

<script>
export default {
  name: "todo-item",
  props: {
    item: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      id: this.item.id,
      title: this.item.title,
      completed: this.item.completed,
    };
  },
  methods: {
    removeTodo(index) {
      this.$emit("removedTodo", index);
    },
    checkTodo() {
      this.$emit("check");
    },
  },
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
