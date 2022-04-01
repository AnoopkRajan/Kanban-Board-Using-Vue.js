<template>
  <span :style="{ background: color }">
    <slot></slot>
  </span>
</template>

<script>
export default {
  props: {
    color: {
      type: String,
      default: "#fef",
    },
  },
};
</script>
