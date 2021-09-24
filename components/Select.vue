<template>
  <select
    :class="['select', {'select_opened': opened}]"
    @change="$emit('input', $event.target.value)"
    @click="$emit('click')"
    @blur="$emit('blur')"
  >
    <option
      v-for="option in options"
      :key="option.value"
      :value="option.value"
      :selected="selected === option.value"
      class="select__option"
    >
      {{ option.text }}
    </option>
  </select>
</template>

<script>
export default {
  props: {
    selected: {
      type: String,
      default: '',
    },
    options: {
      type: Array,
      default: () => [],
    },
    opened: {
      type: Boolean,
      default: false,
    },
  },
  emits: ['click', 'blur', 'input'],

};
</script>

<style lang="scss" scoped>
@import '@/assets/blocks/select.scss';
</style>
