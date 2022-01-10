<template>
  <main 
    class="product"
    @mouseenter="visible = true"
    @mouseleave="visible = false"
  >
    <button 
      v-if="visible"  
      @click="removeItem"
    >
      <img src="../assets/delete-icon.svg" alt="">
    </button>
    <div class="product-content">
      <img  class="bg-img" :src="product.productLinkToImage">
      <span id="product-name" :title="product.productName">{{product.productName}}</span>
      <span id="product-description" :title="product.productDescription">{{product.productDescription}}</span>
      <span id="product-price">{{product.productPrice.toLocaleString()}} руб.</span>
    </div>
  </main>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      default: () => ({
        productName: "Наименование товара",
        productDescription: `Довольно-таки интересное описание 
          товара в несколько строк. Довольно-таки 
          интересное описание товара в несколько строк`,
        price: (10000).toLocaleString(),
        productLinkToImage: "https://photoprocenter.ru/upload/Products/modelId7869/51763ccd5f8f4.jpg"
      }),
    },
  },
  data: () => ({
    visible: false,
  }),

  methods: {
    /**
     * Метод для имитации 
     * события removeItem (удаление товара)
     */
    removeItem() {
      this.$emit('removeItem', this.product.id);
    }
  }

  
}
</script>
