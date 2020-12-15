<template>
  <div class="body">
    <logo class="logo" />
    <input
      class="input"
      type="text"
      placeholder="Skriv din todo här..."
      v-model="todoInput"
      @keyup.enter="addTodo"
    />
    <button class="button" v-on:click="addTodo">Lägg till todo</button>

    <transition-group
      name="fade"
      enter-active-class="animated fadeInUp"
      leave-active-class="animated fadeOutDown"
    >
      <todo-items
        v-for="(item, index) in todoList"
        :key="item.id"
        :item="item"
        :index="index"
        v-bind:checked="checkTodo"
        @removedTodo="removeTodo"
      >
      </todo-items>
    </transition-group>
    <div class="info-div">
      <div>Du har {{ itemsLeft }} uppgift kvar att göra</div>
    </div>
  </div>
</template>

<script>
import Logo from "./Logo.vue";
import TodoItems from "./TodoItems";

export default {
  name: "todo-list",
  components: {
    Logo: Logo,
    TodoItems: TodoItems,
  },
  data() {
    return {
      todoInput: "",
      idTodo: "",
      todoList: [],
    };
  },
  methods: {
    addTodo() {
      if (this.todoInput.trim().length == 0) {
        return;
      }
      this.todoList.push({
        id: this.idTodo,
        title: this.todoInput,
        completed: this.false,
      });

      this.todoInput = "";
      this.idTodo++;
    },
    removeTodo(index) {
      this.todoList.splice(index, 1);
    },
    checkTodo(item) {
      item.completed = !item.completed;
    },
  },
  computed: {
    itemsLeft() {
      return this.todoList.filter((item) => !item.completed).length;
    },
  },
};
</script>

<style scoped>
@import url("https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css");
* {
  box-sizing: border-box;
  margin: 0 auto;
}
.body {
  box-shadow: 0px 0px 18px 8px rgba(0, 0, 0, 0.842);
  max-width: 400px;
  height: 500px;
  margin: auto;
}
.logo {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: auto;
}
.input {
  width: 401px;
  height: 30px;
  border: 0.2rem solid rgba(0, 0, 0, 0.842);
  color: rgba(0, 0, 0, 0.842);
  margin-top: 1rem;
  margin-bottom: -2px;
  margin-left: -0.3px;
  border-radius: 3px;
  text-align: center;
}
.button {
  background-color: rgba(0, 0, 0, 0.842);
  outline: 0;
  border: 0;
  border-radius: 3px;
  width: 400px;
  height: 30px;
  color: antiquewhite;
  cursor: pointer;
}
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
.info-div {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 12px;
  margin-top: 20px;
  border-top: 0.1rem dotted lightgrey;
}
</style>
