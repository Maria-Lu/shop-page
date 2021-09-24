<template>
  <article class="card">
    <button
      class="button card__button"
      type="reset"
      @click="$emit('delete-card', card.id)"
    />
    <img
      class="card__image"
      :src="card.image"
      :alt="card.title"
    >
    <div class="card__container">
      <h2 class="card__title">
        {{ card.title }}
      </h2>
      <p class="card__description">
        {{ card.description }}
      </p>
    </div>
    <p class="card__price">
      {{ formattedPrice }} руб.
    </p>
  </article>
</template>

<script>
export default {
  props: {
    card: {
      type: Object,
      default: () => {},
    },
  },
  emits: ['delete-card'],
  computed: {
    formattedPrice() {
      return this.card.price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ' ');
    },
  },
  methods: {
    deleteCard(id) {
      this.$emit('delete-card', id);
    },
  },

};
</script>

<style lang="scss" scoped>
@import '@/assets/blocks/card.scss';
@import '@/assets/blocks/button.scss';
</style>
