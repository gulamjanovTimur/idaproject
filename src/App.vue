<template>
  <div id="app" class="app">
    <div class="app-content app__content">
      <div class="app-content__header app-header">
        <h2 class="app-header__title">Добавление товара</h2>
        <div class="app-header__select app-select">
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
      <div class="app-content__body app-body">
        <CreateProduct />
        <div class="app-body__products app-products">
          <ProductItem
            :key="index"
            v-for="(item, index) in sortProductsTest"
            :product="item"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CreateProduct from "./components/CreateProduct";
import ProductItem from "./components/ProductItem";
export default {
  name: "App",
  components: {
    CreateProduct,
    ProductItem,
  },
  data() {
    return {
      selectSort: "name",
      products: [
        {
          name: "Абд товар",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 7000,
          linkImg: "https://klike.net/uploads/posts/2019-05/1556708032_1.jpg",
        },
        {
          name: "Наименование товара",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 10000,
          linkImg: "https://klike.net/uploads/posts/2019-05/1556708032_1.jpg",
        },
        {
          name: "ЯБВ товар",
          description:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 5000,
          linkImg: "https://klike.net/uploads/posts/2019-05/1556708032_1.jpg",
        },
      ],
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
    sortProductsTest() {
      return this.sortProducts(this.products);
    },
  },
  methods: {
    sortProducts() {
      if (this.selectSort === "name") {
        return this.products.sort((a, b) => {
          if (a.name > b.name) {
            return 1;
          }
          if (a.name < b.name) {
            return -1;
          }
          return 0;
        });
      }
      if (this.selectSort === "priceMin") {
        return this.products.sort((a, b) => {
          if (a.price > b.price) {
            return 1;
          }
          if (a.price < b.price) {
            return -1;
          }
          return 0;
        });
      }
      if (this.selectSort === "priceMax") {
        return this.products.sort((a, b) => {
          if (a.price < b.price) {
            return 1;
          }
          if (a.price > b.price) {
            return -1;
          }
          return 0;
        });
      }
    },
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
.app {
  padding: 30px;
  min-height: 100vh;
  box-sizing: border-box;
  background-color: #e5e5e5;
  &__content {
    max-width: 1320px;
    margin: 0 auto;
  }
}
.app-header {
  display: flex;
  justify-content: space-between;
  &__title {
    color: #3f3f3f;
    font-size: 28px;
    margin-top: 0;
    margin-bottom: 16px;
  }
}
.app-body {
  display: flex;
  &__products {
    margin-left: 16px;
  }
}
.app-products {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 20px;
  height: 100%;
}
body {
  margin: 0;
}

//CUSTOM SELECT
select {
  appearance: none;
  outline: 0;
  box-shadow: none;
  flex: 1;
  padding: 10px 16px;
  color: #fff;
  background-color: #fffefb;
  cursor: pointer;
  color: #b4b4b4;
  border: none;
  outline: none;
  font-size: 12px;
}
.app-select {
  position: relative;
  display: flex;
  height: 36px;
  border-radius: 0.25em;
  overflow: hidden;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  &::after {
    content: url(assets/images/expand.svg);
    position: absolute;
    top: 7px;
    right: 0;
    transition: 0.25s all ease;
    pointer-events: none;
  }
}
</style>
