<template>
  <div class="skeleton"></div>
</template>

<script>
export default {
  name: 'AnimatedPlaceholder',
  props: {
    width: { type: String, default: '100%' },
    height: { type: String, default: '8px' },
    bgColor: { type: String, default: '#334155' },
    rounded: { type: String, default: '4px' },
    mt: { type: String, default: '0' },
    mb: { type: String, default: '0' },
  }
}
</script>

<style scoped>
.skeleton {
  width: v-bind(width);
  height: v-bind(height);
  background-color: v-bind(bgColor);
  border-radius: v-bind(rounded);
  margin-top: v-bind(mt);
  margin-bottom: v-bind(mb);
  animation: pulse 1.5s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

@keyframes pulse {

  0%,
  100% {
    opacity: 1;
  }

  50% {
    opacity: .5;
  }
}
</style>