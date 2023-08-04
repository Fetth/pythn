<template>
  <button>
    {{icon}} {{text}}
  </button>
</template>

<script>
export default {
  props: {
    text: String,
    icon: String
  }
}
</script>