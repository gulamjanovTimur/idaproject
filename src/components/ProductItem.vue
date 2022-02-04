<template>
  <div class="product">
    <div
      :style="`background-image:url(${product.linkImg})`"
      :alt="product.name"
      class="product__img"
    ></div>
    <div class="product__name">{{ product.name }}</div>
    <div class="product__description">{{ product.description }}</div>
    <div class="product__price">{{ product.price }} руб.</div>
  </div>
</template>

<script>
export default {
  name: "ProductItem",
  props: {
    product: {
      type: Object,
      default: () => {},
    },
  },
};
</script>

<style lang="scss" scoped>
.product {
  border-radius: 4px;
  color: #3f3f3f;
  overflow: hidden;
  background-color: #fffefb;
  cursor: pointer;
  &__img {
    height: 200px;
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
  }
  &__name {
    font-size: 20px;
    font-weight: 600;
    margin: 16px;
  }
  &__description {
    font-size: 16px;
    margin: 16px 16px 32px;
  }
  &__price {
    font-weight: bold;
    font-size: 24px;
    margin: 24px 16px;
  }
}
</style>
