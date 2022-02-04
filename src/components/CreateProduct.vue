<template>
  <form class="create-product-form">
    <div
      class="create-product-form__label create-product-form__label--required"
    >
      Наименование товара
    </div>
    <input
      placeholder="Введите наименование товара"
      class="create-product-form__input"
      v-model="form.name"
    />
    <div
      class="create-product-form__label create-product-form__label--required"
    >
      Описание товара
    </div>
    <textarea
      placeholder="Введите описание товара"
      class="create-product-form__area"
      v-model="form.description"
    />
    <div
      class="create-product-form__label create-product-form__label--required"
    >
      Ссылка на изображение товара
    </div>
    <input
      placeholder="Введите ссылку"
      class="create-product-form__input"
      v-model="form.linkImg"
    />
    <div
      class="create-product-form__label create-product-form__label--required"
    >
      Цена товара
    </div>
    <input
      placeholder="Введите цену"
      class="create-product-form__input"
      v-model="form.price"
    />
    <button class="create-product-form__btn">Добавить товар</button>
  </form>
</template>
<script>
export default {
  name: "CreateProduct",
  data() {
    return {
      form: {
        price: "",
        name: "",
        description: "",
        linkImg: "",
      },
    };
  },
};
</script>

<style lang="scss" scoped>
.create-product-form {
  width: 332px;
  min-width: 332px;
  padding: 24px;
  background-color: #fffefb;
  box-sizing: border-box;
  border-radius: 4px;
  &__label {
    font-size: 10px;
    color: #49485e;
    margin-bottom: 4px;
    position: relative;
    width: fit-content;
    &--required {
      &::after {
        content: "";
        display: block;
        height: 4px;
        width: 4px;
        background-color: #ff8484;
        position: absolute;
        top: 0;
        border-radius: 50%;
        right: -5px;
      }
    }
  }
  &__input {
    box-sizing: border-box;
    padding: 10px 16px;
    font-size: 12px;
    height: 36px;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border: none;
    width: 100%;
    margin-bottom: 16px;
    border-radius: 4px;
    color: #3f3f3f;
    &::placeholder {
      color: #b4b4b4;
    }
  }
  &__area {
    padding: 10px 16px;
    margin-bottom: 16px;
    font-size: 12px;
    border-radius: 4px;
    border: none;
    color: #3f3f3f;
    box-sizing: border-box;
    width: 100%;
    height: 108px;
    resize: none;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    &::placeholder {
      color: #b4b4b4;
    }
  }
  &__btn {
    background-color: #eeeeee;
    width: 100%;
    height: 36px;
    border: none;
    font-size: 12px;
    color: #b4b4b4;
    border-radius: 10px;
  }
}
</style>
