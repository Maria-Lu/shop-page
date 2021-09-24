<template>
  <form
    id="add-card-form"
    class="form"
    name="add-card-form"
    novalidate
    @submit.prevent="handleSubmit"
  >
    <label
      class="form__label form__label_required"
      for="card-title"
    >Наименование товара</label>
    <input
      id="card-title"
      v-model.trim="card.title"
      name="title"
      placeholder="Введите наименование товара"
      type="text"
      :class="['form__field', {'form__field_invalid': isTitleError}]"
      @blur="isTitleTouched=true"
    >
    <span :class="['form__error', {'form__error_visible': isTitleError}]">
      {{ error }}
    </span>
    <label
      class="form__label"
      for="card-description"
    >Описание товара</label>
    <textarea
      id="card-description"
      v-model.trim="card.description"
      name="description"
      placeholder="Введите описание товара"
      class="form__field form__field_type_description"
    />
    <label
      class="form__label form__label_required"
      for="card-image"
    >Ссылка на изображение товара</label>
    <input
      id="card-title"
      v-model.trim="card.image"
      name="image"
      placeholder="Введите ссылку"
      type="url"
      :class="['form__field', {'form__field_invalid': isImageError}]"
      @blur="isImageTouched=true"
    >
    <span :class="['form__error', {'form__error_visible': isImageError}]">
      {{ error }}
    </span>
    <label
      class="form__label form__label_required"
      for="card-price"
    >Цена товара</label>
    <input
      id="card-price"
      v-model.trim="card.price"
      name="price"
      placeholder="Введите цену"
      type="text"
      :class="['form__field', {'form__field_invalid': isPriceError}]"
      @blur="isPriceTouched = true, card.price = formattedPrice"
      @focus="card.price = unformattedPrice"
    >
    <span :class="['form__error', {'form__error_visible': isPriceError}]">
      {{ error }}
    </span>
    <button
      :class="['button', 'form__button', {'form__button_disabled': !isFormValid}]"
      type="submit"
      :disabled="!isFormValid"
    >
      Добавить товар
    </button>
  </form>
</template>

<script>
import uniqueId from 'lodash.uniqueid';

export default {
  emits: ['add-card'],
  data() {
    return {
      card: {
        title: '',
        description: '',
        image: '',
        price: '',
      },
      isTitleTouched: false,
      isImageTouched: false,
      isPriceTouched: false,
      error: 'Поле является обязательным',
    };
  },
  computed: {
    formattedPrice() {
      return this.card.price.replace(/\B(?=(\d{3})+(?!\d))/g, ' ');
    },
    unformattedPrice() {
      return this.card.price.replace(/\s/g, '');
    },
    isTitleValid() {
      return this.card.title.length > 0;
    },
    isImageValid() {
      return /^(https?:\/\/)?([\w-]+\.[\w-]+)\S*$/.test(this.card.image);
    },
    isPriceValid() {
      return /^\d{1,3}(?:\s*\d{3})*$/.test(this.card.price);
    },
    isTitleError() {
      return !this.isTitleValid && this.isTitleTouched;
    },
    isImageError() {
      return !this.isImageValid && this.isImageTouched;
    },
    isPriceError() {
      return !this.isPriceValid && this.isPriceTouched;
    },
    isFormValid() {
      return this.isTitleValid && this.isImageValid && this.isPriceValid;
    },
  },
  methods: {
    handleSubmit() {
      if (this.isFormValid) {
        const newCard = {
          id: uniqueId(),
          title: this.card.title,
          image: this.card.image,
          description: this.card.description,
          price: +this.unformattedPrice,
        };
        this.$emit('add-card', newCard);
        this.card.title = '';
        this.card.description = '';
        this.card.image = '';
        this.card.price = '';
        this.isTitleTouched = false;
        this.isImageTouched = false;
        this.isPriceTouched = false;
      }
    },

  },
};
</script>

<style lang="scss" scoped>
  @import '@/assets/blocks/button.scss';
  @import '@/assets/blocks/form.scss';
</style>
