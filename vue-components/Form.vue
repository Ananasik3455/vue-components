<template>
  <form 
    class="form"
    @submit.prevent="processForm"
  >
    <cu-input
      v-model="product.productName"
      :errorIndicator="error.productName"
      :errorMessage="'Поле является обязательным'"
      placeholder="Введите наименование товара"
      label="Наименование товара"
      type="text"
      @input="validate(product.productName, 'productName')"
    />

    <div class="textarea-container">
      <label for="productDescription">Описание товара</label>
      <textarea 
        v-model="product.productDescription" 
        :class="[error.productDescription ? errorClass : '']"
        placeholder="Введите описание товара"
        name="productDescription" 
        class="textarea"
        @input="validate(product.productDescription, 'productDescription')"
        />
      <span id="error" v-if="error.productDescription"> Поле является обязательным </span>
    </div>

    <cu-input
      v-model="product.productLinkToImage"
      :errorIndicator="error.productLinkToImage"
      :errorMessage="'Поле является обязательным'"
      
      placeholder="Введите ссылку"
      label="Ссылка на изображение"
      type="text"
      @input="validate(product.productLinkToImage, 'productLinkToImage')"
    />

    <cu-input
      v-model="modelNumber"
      :type="indicatorChange ? 'number' : 'text'"
      :errorIndicator="error.productPrice"
      :errorMessage="'Поле является обязательным'"
      placeholder="Введите цену"
      label="Цена товара"
      @focus="indicatorChange = true"
      @blur="indicatorChange = false"
      @input="validate(product.productPrice, 'productPrice')"
    />

      <input 
        :disabled="isValid"
        :class="[isValid ? disabledClass : defaultClass ]"
        type="submit" 
        value="Добавить товар"
      >
  </form>
</template>

<script>
import CuInput from './CuInput.vue';

export default {
  components: {
    CuInput,
  },
  data: () => ({
    disabledClass: 'disabled-input',
    defaultClass: 'default-input',
    errorClass: 'error-input',
    product: {
      productName: '',
      productDescription: '',
      productLinkToImage: '',
      productPrice: 0,
    },
    indicatorChange: false,
    error: {
      productName: false,
      productDescription: false,
      productLinkToImage: false,
      productPrice: false,
    },
  }),

  methods: {
    /**
    Сбор данных и вызов события для добавления нового товара
     */
    processForm() {
      this.$emit('addproduct', Object.assign({
        id: Date.now(),
      }, this.product));
      this.product.productName = "";
      this.product.productDescription = "";
      this.product.productLinkToImage = "";
      this.product.productPrice = 0;
    },

    /**
     * Метод для изменения булевых значений ошибок
     */
    validate(item, errorIdx) {
      this.error[errorIdx] = !item;
      console.log(this.error[errorIdx]);
    },
  },

  computed: {
    /**
     * Свойство для обработки свойства товара  
     */
    modelNumber: {
      get() {
        return this.indicatorChange ? this.product.productPrice : this.product.productPrice.toLocaleString();
      },
      set(value) {
        this.product.productPrice = +value.replace(/\s/g, "");
        if (this.product.productPrice < 0 || this.product.productPrice > 999999999) {
          this.product.productPrice = 1;
        }
        this.$emit('input', this.product.productPrice);
      },
    },

    /**
     * Свойство для проверки на наличие ошибок 
     */
    isValid() {
      return Object.values(this.product).some(item => item == false);
    },
  },
}
</script>
