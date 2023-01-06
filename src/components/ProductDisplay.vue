<template>
  <div :class="['content', renderClassByProductCategory(product?.category)]">
    <ProductSkeleton v-if="isLoading" />

    <div v-else-if="product" :class="['product', renderClassByProductCategory(product.category)]">
      <div class="product__img">
        <img :src="product.image" />
      </div>
      <div class="product__content">
        <h1 class="product__title">{{ product.title }}</h1>
        <div class="product__header-flex">
          <p class="product__category">{{ product.category }}</p>
          <div class="product__rating">
            <p class="product__rating-score">{{ product.rating.rate }}/5</p>
            <div class="star-rating">
              <div class="star-content">
                <div class="bullet"></div>
                <div class="bullet"></div>
                <div class="bullet"></div>
                <div class="bullet"></div>
                <div class="bullet"></div>
              </div>
              <div class="star-content star-content-fill" :style="{ width: `${(product.rating.rate / 5) * 100}%` }">
                <div class="bullet"></div>
                <div class="bullet"></div>
                <div class="bullet"></div>
                <div class="bullet"></div>
                <div class="bullet"></div>
              </div>
            </div>
          </div>
        </div>
        <p class="product__description">{{ product.description }}</p>
        <p class="product__price">${{ product.price }}</p>
        <div class="cta">
          <button class="btn btn-solid">Buy now</button>
          <button @click="increaseProductIdHandler" class="btn btn-outline">Next product</button>
        </div>
      </div>
    </div>

    <div v-else class="product unavailable">
      <div>
        <p class="message">This product is unavailable to show</p>
        <button @click="increaseProductIdHandler" class="btn btn-outline">Next product</button>
      </div>
    </div>
  </div>
</template>

<script>
import ProductSkeleton from './ProductSkeleton.vue'

export default {
  name: 'ProductDisplay',
  components: { ProductSkeleton },
  data() {
    return {
      product: null,
      currentProductId: 1,
      isLoading: false,
      availableCategories: ["men's clothing", "women's clothing"]
    }
  },
  methods: {
    increaseProductIdHandler() {
      this.currentProductId < 20 ? this.currentProductId++ : this.currentProductId = 1
    },
    productInAvailableCategory(product) {
      return this.availableCategories.includes(product.category)
    },
    renderClassByProductCategory(productCategory) {
      switch (productCategory) {
        case "men's clothing": return 'men'
        case "women's clothing": return 'women'
        default: return 'unavailable '
      }
    },
    async fetchProduct(productId) {
      this.product = null
      this.isLoading = true

      try {
        const res = await fetch(`https://fakestoreapi.com/products/${productId}`)
        const productData = await res.json();
        if (this.availableCategories.includes(productData.category)) {
          this.product = productData
        }
      } catch (error) {
        console.log(error.message)
      } finally {
        this.isLoading = false
      }
    }
  },
  watch: {
    currentProductId: {
      handler() {
        this.fetchProduct(this.currentProductId)
      },
      immediate: true
    }
  }
}
</script>