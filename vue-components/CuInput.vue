<template>
  <div class="input">
    <label for="input-el">{{label}}</label>
    <input
      v-model="model"
      :placeholder="placeholder" 
      :type="type" 
      name="input-el"
      :class="[errorIndicator ? errorClass : '' ]" 
      @focus="$emit('focus')"
      @blur="$emit('blur')"
    >
    <span id="error" v-if="errorIndicator"> {{errorMessage}} </span>
  </div>
</template>

<script>
export default {
  props: ['value', 'label', 'placeholder', 'type', 'errorMessage', 'errorIndicator'],
  data: () => ({
    errorClass: 'error-input',
  }),

  computed: {
    model: {
      get() {
        return this.value;
      },
      set(newVal) {
        this.$emit('input', newVal);
      },
    }
  }
}
</script>