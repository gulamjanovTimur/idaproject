<template>
  <div class="products-list">
    <div class="select-wrapper">
      <div class="products-list__select">
        <select v-model="selectSort">
          <option
            :key="option.value"
            v-for="option in options"
            :value="option.value"
          >
            {{ option.label }}
          </option>
        </select>
      </div>
    </div>
    <transition-group
      tag="div"
      class="products-list__items products"
      name="list"
    >
      <ProductItem
        @delete-product="deleteProduct"
        :key="item.id"
        v-for="(item, index) in sortProducts"
        :product="item"
        :index="index"
      />
    </transition-group>
  </div>
</template>
<script>
import ProductItem from "./ProductItem.vue";
export default {
  name: "ProductsList",
  components: { ProductItem },
  props: {
    products: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      selectSort: "name",
      options: [
        {
          value: "name",
          label: "По наименованию",
        },
        {
          value: "priceMin",
          label: "По цене min (от меньшего к большему)",
        },
        {
          value: "priceMax",
          label: "По цене max (от большего к меньшему)",
        },
      ],
    };
  },
  computed: {
    sortProducts() {
      return this.sortProductsFunc(this.products);
    },
  },
  methods: {
    deleteProduct(index) {
      this.$emit("delete-product", index);
    },
    sortProductsFunc() {
      if (this.selectSort === "name") {
        return this.products.sort((a, b) => {
          if (a.name.toLowerCase() > b.name.toLowerCase()) {
            return 1;
          }
          if (a.name.toLowerCase() < b.name.toLowerCase()) {
            return -1;
          }
          return 0;
        });
      }
      if (this.selectSort === "priceMin") {
        return this.products.sort((a, b) => {
          if (Number(a.price) > Number(b.price)) {
            return 1;
          }
          if (Number(a.price) < Number(b.price)) {
            return -1;
          }
          return 0;
        });
      }
      if (this.selectSort === "priceMax") {
        return this.products.sort((a, b) => {
          if (Number(a.price) < Number(b.price)) {
            return 1;
          }
          if (Number(a.price) > Number(b.price)) {
            return -1;
          }
          return 0;
        });
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.products-list {
  display: flex;
  flex-direction: column;
  &__items {
    flex: 1;
    margin-left: 16px;
  }
  &__select {
    position: relative;
    height: 36px;
    float: right;
    width: fit-content;
    border-radius: 0.25em;
    overflow: hidden;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    &::after {
      content: url(../assets/images/expand.svg);
      position: absolute;
      top: 7px;
      right: 8px;
      transition: 0.25s all ease;
      pointer-events: none;
    }
  }
}
.products {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 20px;
  height: 100%;
}
// CUSTOM SELECT
.select-wrapper {
  margin-bottom: 8px;
}
select {
  height: 100%;
  appearance: none;
  outline: 0;
  box-shadow: none;
  flex: 1;
  padding: 10px 30px 10px 16px;
  color: #fff;
  background-color: #fffefb;
  cursor: pointer;
  color: #b4b4b4;
  border: none;
  outline: none;
  font-size: 12px;
}
// ANIMATIONS
.list-item {
  display: inline-block;
  margin-right: 10px;
}
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
@media (max-width: 1025px) {
  .products-list {
    &__items {
      margin-left: 0;
    }
  }
  .select-wrapper {
    margin-bottom: 20px;
  }
  .products {
    grid-template-columns: 1fr 1fr;
  }
}
</style>
