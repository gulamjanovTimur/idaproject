<template>
  <div class="create-product">
    <h2 class="create-product__title">Добавление товара</h2>
    <form @submit.prevent="createProduct" class="create-product-form">
      <div :key="index" v-for="(item, index) in form">
        <div
          :class="{ 'create-product-form__label--required': item.required }"
          class="create-product-form__label"
        >
          {{ item.label }}
        </div>
        <div class="input-wrapper" v-if="item.type === 'input'">
          <input
            :class="{
              'input-wrapper__input--validate-error': errors[item.key],
            }"
            :placeholder="item.placeholder"
            class="input-wrapper__input"
            :type="item.key === 'price' ? 'number' : 'text'"
            v-model="item.model"
          />
          <span class="input-wrapper__error" v-if="errors[item.key]">{{
            errors[item.key]
          }}</span>
        </div>
        <textarea
          v-else
          :placeholder="item.placeholder"
          class="create-product-form__area"
          v-model="item.model"
        />
      </div>
      <button
        :class="{
          'create-product-form__btn--validate-success':
            form.name.model && form.price.model && form.linkImg.model,
        }"
        class="create-product-form__btn"
      >
        Добавить товар
      </button>
    </form>
  </div>
</template>
<script>
export default {
  name: "CreateProduct",
  data() {
    return {
      form: {
        name: {
          label: "Наименование товара",
          required: true,
          model: "",
          type: "input",
          placeholder: "Введите наименование товара",
          key: "name",
        },
        description: {
          label: "Описание товара",
          required: false,
          model: "",
          type: "area",
          placeholder: "Введите описание товара",
          key: "description",
        },
        linkImg: {
          label: "Ссылка на изображение товара",
          required: true,
          model: "",
          type: "input",
          placeholder: "Введите ссылку",
          key: "linkImg",
        },
        price: {
          label: "Цена товара",
          required: true,
          model: "",
          type: "input",
          placeholder: "Введите цену",
          key: "price",
        },
      },
      errors: {},
    };
  },
  methods: {
    createProduct() {
      if (
        this.form.price.model &&
        this.form.name.model &&
        this.form.linkImg.model
      ) {
        this.errors = {};
        this.$emit("add-product", {
          name: this.form.name.model,
          price: this.form.price.model,
          linkImg: this.form.linkImg.model,
          description: this.form.description.model,
        });
      } else {
        this.errors = {};
        for (const key in this.form) {
          const element = this.form[key];
          if (element.required && !element.model) {
            this.errors = {
              ...this.errors,
              [key]: "Поле является обязательным",
            };
          }
        }
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.create-product {
  &__title {
    line-height: 1;
    color: #3f3f3f;
    font-size: 28px;
    margin-top: 0;
    margin-bottom: 16px;
  }
}
.create-product-form {
  width: 332px;
  max-height: 100%;
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
    &:focus {
      outline: 1px solid green;
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
    margin-top: 8px;
    cursor: pointer;
    transition: 0.3s;
    &:hover {
      background-color: #b4b4b4;
      color: #eeeeee;
    }
    &:active {
      background-color: #8d8d8d;
      color: #ffffff;
    }
    &--validate-success {
      background-color: #7bae73;
      color: #ffffff;
      &:hover {
        background-color: #2fa71c;
        color: #ffffff;
      }
      &:active {
        background-color: #107a00;
        color: #ffffff;
      }
    }
  }
}
.input-wrapper {
  position: relative;
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
    &--validate-error {
      outline: 1px solid #ff8484 !important;
    }
    &::placeholder {
      color: #b4b4b4;
    }
    &:focus {
      outline: 1px solid green;
    }
  }
  &__error {
    position: absolute;
    bottom: 1px;
    left: 0;
    color: #ff8484;
    font-size: 8px;
  }
}
// delete arrows input type
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type="number"] {
  -moz-appearance: textfield;
}
@media (max-width: 1025px) {
  .create-product-form {
    width: 100%;
    min-width: 100%;
    padding: 16px;
  }
}
</style>
