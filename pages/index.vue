<template>
  <div class="page">
    <header class="header page__section">
      <h1 class="header__title">
        Добавление товара
      </h1>
      <Select
        v-model="selected"
        :options="options"
        :opened="opened"
        @click="toggleDropdown"
        @blur="unfocuseDropdown"
      >
        />
      </select>
    </header>
    <main class="content page__section">
      <Form @add-card="addCard" />
      <section class="cards">
        <Card
          v-for="card of selectedCards"
          :key="card.id"
          :card="card"
          @delete-card="deleteCard"
        />
      </section>
    </main>
  </div>
</template>

<script>
import uniqueId from 'lodash.uniqueid';
import Select from '@/components/Select.vue';
import Card from '@/components/Card.vue';
import Form from '@/components/Form.vue';

export default {
  components: {
    Select, Card, Form,
  },
  data() {
    return {
      opened: false,
      selected: 'default',
      options: [
        { text: 'По умолчанию', value: 'default' },
        { text: 'По цене min', value: 'min-price' },
        { text: 'По цене max', value: 'max-price' },
        { text: 'По названию', value: 'name' },
      ],
      cards: [
        {
          id: uniqueId(),
          title: 'Прекрасный товар',
          image: 'https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 15000,
        },
        {
          id: uniqueId(),
          title: 'Великолепный товар',
          image: 'https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 16000,
        },
        {
          id: uniqueId(),
          title: 'Изумительный товар',
          image: 'https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 12000,
        },
        {
          id: uniqueId(),
          title: 'Чудесный товар',
          image: 'https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 17000,
        },
        {
          id: uniqueId(),
          title: 'Славный товар',
          image: 'https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000,
        },
        {
          id: uniqueId(),
          title: 'Замечательный товар',
          image: 'https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 13000,
        },
        {
          id: uniqueId(),
          title: 'Роскошный товар',
          image: 'https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 14000,
        },
        {
          id: uniqueId(),
          title: 'Необыкновенный товар',
          image: 'https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 18000,
        },
        {
          id: uniqueId(),
          title: 'Отличный товар',
          image: 'https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80',
          description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 11000,
        },
      ],
    };
  },
  computed: {
    selectedCards() {
      const cards = this.cards.slice();
      if (this.selected === 'min-price') {
        return cards.sort((a, b) => (a.price > b.price ? 1 : -1));
      }
      if (this.selected === 'max-price') {
        return cards.sort((a, b) => (a.price > b.price ? -1 : 1));
      }
      if (this.selected === 'name') {
        return cards.sort((a, b) => {
          const nameA = a.title.toLowerCase();
          const nameB = b.title.toLowerCase();
          if (nameA < nameB) return -1;
          if (nameA > nameB) return 1;
          return 0;
        });
      } return this.cards;
    },
  },
  methods: {
    toggleDropdown() {
      this.opened = !this.opened;
    },
    unfocuseDropdown() {
      this.opened = false;
    },
    deleteCard(id) {
      this.cards = this.cards.filter((card) => card.id !== id);
    },
    addCard(cardData) {
      this.cards.unshift(cardData);
    },
  },
};
</script>

<style lang="scss" scoped>
@import '@/assets/blocks/page.scss';
@import '@/assets/blocks/header.scss';
@import '@/assets/blocks/content.scss';
@import '@/assets/blocks/cards.scss';
</style>
