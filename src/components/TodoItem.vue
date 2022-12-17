<template>
  <li>
    <my-input
      :class="!todo.done || 'done'"
      v-model="todoValue"
      :disabled="!isEdit"
    />
    <div class="controls">
      <my-checkbox :checked="todo.done" @change="$emit('setDone', todo.id)" />
      <my-button @click="edit">{{ editOrSave }}</my-button>
      <my-button @click="$emit('delete', todo.id)"
        ><i class="fa-solid fa-trash"></i
      ></my-button>
    </div>
  </li>
</template>

<script>
import MyButton from "./UI/MyButton.vue";
import MyCheckbox from "./UI/MyCheckbox.vue";
import MyInput from "./UI/MyInput.vue";
export default {
  components: { MyButton, MyCheckbox, MyInput },
  name: "TodoItem",
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      isEdit: false,
      todoValue: this.todo.name,
    };
  },
  computed: {
    editOrSave() {
      return this.isEdit ? "save" : "edit";
    },
  },
  methods: {
    edit() {
      this.isEdit = !this.isEdit;
      if (!this.isEdit) {
        this.$emit("change", {
          ...this.todo,
          name: this.todoValue,
        });
      }
    },
  },
};
</script>

<style lang="sass" scoped>
li
  display: flex
  justify-content: space-between
  align-items: center
  margin-bottom: 1rem
  .done
    text-decoration: line-through
  .controls
    display: flex
    align-items: center
    .my-button
      margin-left: .2rem
</style>
