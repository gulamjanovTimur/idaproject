<template>
  <div class="product">
    <div @click.stop="deleteProduct" class="product__delete product-delete">
      <img src="../assets/images/trash.svg" alt="delete-icon" />
    </div>
    <div class="product__content product-content">
      <div
        :style="`background-image:url(${product.linkImg})`"
        :alt="product.name"
        class="product-content__img"
      ></div>
      <div class="product-content__text product-text">
        <div>
          <div class="product-text__name">{{ product.name }}</div>
          <div class="product-text__description">
            {{ product.description }}
          </div>
        </div>
        <div class="product-text__price">
          {{ divideAmount(product.price) }} руб.
        </div>
      </div>
    </div>
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
    index: {
      type: Number,
      default: () => 100,
    },
  },
  methods: {
    divideAmount(num) {
      if (num) {
        try {
          const numA = num.toString();
          return numA.replace(/(\d{1,3}(?=(?:\d\d\d)+(?!\d)))/g, "$1" + " ");
        } catch (e) {
          throw "Function divideAmount got error: \n " + e;
        }
      } else {
        return 0;
      }
    },
    deleteProduct() {
      this.$emit("delete-product", this.index);
    },
  },
};
</script>

<style lang="scss" scoped>
.product {
  word-break: break-word;
  border-radius: 4px;
  color: #3f3f3f;
  background-color: #fffefb;
  cursor: pointer;
  position: relative;
  transition: 0.3s;
  &:hover &__delete {
    opacity: 1;
  }
  &__delete {
    transition: 0.3s;
    opacity: 0;
    width: 32px;
    height: 32px;
    border-radius: 10px;
    position: absolute;
    top: -10px;
    right: -10px;
  }
}
.product-content {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  position: relative;
  height: 100%;
  &__img {
    border-top-left-radius: 4px;
    border-top-right-radius: 4px;
    height: 200px;
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
  }
}
.product-text {
  flex: 1;
  display: flex;
  justify-content: space-between;
  flex-direction: column;
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
    margin: 0 16px 24px;
  }
}
.product-delete {
  z-index: 999;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #ff8484;
}
@media (max-width: 1025px) {
  .product {
    &__delete {
      opacity: 1;
    }
  }
  .product-text {
    &__name {
      margin: 8px;
      font-size: 14px;
    }
    &__description {
      font-size: 12px;
      margin: 8px 8px 16px;
    }
    &__price {
      font-size: 20px;
      margin: 0 8px 12px;
    }
  }
}
</style>
