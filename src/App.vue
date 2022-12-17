<template>
  <div id="app">
    <div class="container">
      <h1>ToDo App</h1>
      <create-todo-form style="width: 100%" @createTodo="createTodo" />
      <ul>
        <draggable v-model="todoList">
          <transition-group>
            <todo-item
              v-for="todo in todoList"
              :key="todo.id"
              :todo="todo"
              @delete="deleteTodo"
              @setDone="changeDoneTodo"
              @change="change"
            />
          </transition-group>
        </draggable>
      </ul>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";
import CreateTodoForm from "./components/CreateTodoForm.vue";
import TodoItem from "./components/TodoItem.vue";
export default {
  components: { CreateTodoForm, TodoItem, draggable },
  name: "App",
  data() {
    return {
      todoList: [],
    };
  },
  mounted() {
    this.todoList = JSON.parse(localStorage.getItem("todoList")) || [];
  },
  watch: {
    todoList(sortedTodoList) {
      localStorage.setItem("todoList", JSON.stringify(sortedTodoList));
    },
  },
  methods: {
    createTodo(todoItem) {
      this.todoList.push(todoItem);
      localStorage.setItem("todoList", JSON.stringify(this.todoList));
    },
    deleteTodo(id) {
      this.todoList = this.todoList.filter((item) => item.id !== id);
      localStorage.setItem("todoList", JSON.stringify(this.todoList));
    },
    changeDoneTodo(id) {
      const item = this.todoList.find((item) => item.id === id);
      item.done = !item.done;
      localStorage.setItem("todoList", JSON.stringify(this.todoList));
    },
    change(todo) {
      const item = this.todoList.find((item) => item.id === todo.id);
      item.name = todo.name;
      localStorage.setItem("todoList", JSON.stringify(this.todoList));
    },
  },
};
</script>

<style lang="sass">
#app
  font-family: Avenir, Helvetica, Arial, sans-serif
.container
  margin: 0 auto
  max-width: 900px
  display: flex
  flex-direction: column
  align-items: center
  h1
    margin: 0
    margin-bottom: .5rem
  ul
    list-style: none
    max-width: 420px
    width: 100%
    padding: 0
    display: flex
    flex-direction: column
</style>
