<template>
  <input
    class="my-input"
    :value="value"
    @input="(e) => $emit('input', e.target.value)"
    :disabled="disabled"
    type="text"
  />
</template>

<script>
export default {
  name: "MyInput",
  props: {
    value: {
      type: String,
      required: true,
    },
    disabled: {
      type: Boolean,
      required: false,
      default: () => false,
    },
  },
};
</script>

<style lang="sass" scoped>
.my-input
  border: none
  border-bottom: 1px solid #000
  background-color: #fff
  padding: .4rem .7rem
  width: 100%
  font-size: 1.2rem
  &:focus
    outline: none
  &:disabled
    border: none
</style>
