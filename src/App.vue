<template>
  <div id="app" class="app">
    <div class="app-content app__content">
      <CreateProduct
        class="app-content__create-product"
        @add-product="addProduct"
      />
      <ProductsList
        class="app-content__products"
        @delete-product="deleteProduct"
        :products="products"
      />
    </div>
    <Notification :isActive="isActiveAdd" text="Товар добавлен успешно" />
  </div>
</template>

<script>
import CreateProduct from "./components/CreateProduct";
import Notification from "./components/Notification.vue";
import ProductsList from "./components/ProductsList.vue";
export default {
  name: "App",
  components: {
    CreateProduct,
    Notification,
    ProductsList,
  },
  data() {
    return {
      isActiveAdd: false,
      selectSort: "name",
      products: [],
    };
  },
  methods: {
    addProduct(data) {
      this.products.push({ ...data, id: Date.now() });
      localStorage.setItem("products", JSON.stringify(this.products));
      this.isActiveAdd = true;
      setTimeout(() => {
        this.isActiveAdd = false;
      }, 5000);
    },
    deleteProduct(index) {
      this.products.splice(index, 1);
      localStorage.setItem("products", JSON.stringify(this.products));
    },
  },
  mounted() {
    if (localStorage.getItem("products")) {
      this.products = JSON.parse(localStorage.getItem("products"));
    }
  },
};
</script>
<style lang="scss">
@font-face {
  font-family: "Source Sans Pro";
  font-weight: normal;
  src: url("./assets/fonts/SourceSansPro-Regular.ttf");
}
* {
  font-family: Source Sans Pro;
}
body {
  margin: 0;
}
.app {
  padding: 30px;
  min-height: 100vh;
  box-sizing: border-box;
  background-color: #e5e5e5;
  &__content {
    max-width: 1320px;
    margin: 0 auto;
    display: flex;
  }
}
@media (max-width: 1025px) {
  .app {
    padding: 16px;
    &__content {
      flex-direction: column;
    }
  }
  .app-content {
    &__products {
      margin-top: 20px;
    }
  }
}
</style>
