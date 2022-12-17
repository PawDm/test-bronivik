<template>
  <form @submit.prevent="createTodo">
    <my-input v-model="todoName" />
    <my-button type="submit">create</my-button>
  </form>
</template>

<script>
import MyButton from "./UI/MyButton.vue";
import MyInput from "./UI/MyInput.vue";
export default {
  components: { MyButton, MyInput },
  name: "CreateTodoForm",
  data() {
    return {
      todoName: "",
    };
  },
  methods: {
    createTodo() {
      this.$emit("createTodo", {
        id: Date.now(),
        name: this.todoName,
        done: false,
      });
      this.todoName = "";
    },
  },
};
</script>

<style lang="sass" scoped>
form
  max-width: 420px
  display: flex
  justify-content: space-between
  input
    margin-right: .4rem
</style>
