<template>
  <div class="product">
    <div class="product__img">
      <AnimatedPlaceholder width="250px" height="250px" />
    </div>
    <div class="product__content">
      <AnimatedPlaceholder />
      <AnimatedPlaceholder width="70%" mt="8px" />
      <div class="product__header-flex" :style="{ marginTop: '30px' }">
        <AnimatedPlaceholder width="100px" />
        <AnimatedPlaceholder width="25px" />
      </div>
      <div class="product__description" :style="{ minHeight: '100px', marginTop: '20px' }">
        <AnimatedPlaceholder />
        <AnimatedPlaceholder mt="8px" />
        <AnimatedPlaceholder width="80%" mt="8px" />
        <AnimatedPlaceholder width="40%" mt="8px" />
      </div>
      <AnimatedPlaceholder width="100px" height="20px" mt="20px" mb="30px" />
      <div class="cta">
        <AnimatedPlaceholder width="150px" height="40px" :style="{ flex: 1 }" />
        <AnimatedPlaceholder width="150px" height="40px" :style="{ flex: 1 }" />
      </div>
    </div>
  </div>
</template>

<script>
import AnimatedPlaceholder from './AnimatedPlaceholder.vue';

export default {
  name: 'ProductSkeleton',
  components: { AnimatedPlaceholder }
}
</script>