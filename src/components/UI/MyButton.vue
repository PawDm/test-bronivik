<template>
  <button class="my-button" :type="type" @click="$emit('click')">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "MyButton",
  props: {
    type: {
      type: String,
      required: false,
      default: () => "button",
    },
  },
};
</script>

<style lang="sass" scoped>
.my-button
  border: 1px solid #000
  cursor: pointer
  background-color: #fff
  border-radius: 5px
  padding: .4rem .7rem
  text-transform: uppercase
</style>
