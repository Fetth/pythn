<template>
  <button @click="butClick">
    {{icon}}
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: {
    icon: String
  },
  methods: {
    butClick() {
      this.$emit('buttonClicked', 10, 'Button', 20)
    }
  }
}
</script>