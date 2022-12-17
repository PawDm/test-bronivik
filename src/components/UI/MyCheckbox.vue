<template>
  <input
    class="my-checkbox"
    :checked="checked"
    type="checkbox"
    @change="$emit('change')"
  />
</template>

<script>
export default {
  name: "MyCheckbox",
  props: {
    checked: {
      type: Boolean,
      required: true,
    },
  },
};
</script>

<style lang="sass" scoped>
.my-checkbox
  height: 1rem
  width: 1rem
  border: 1px solid red
</style>
