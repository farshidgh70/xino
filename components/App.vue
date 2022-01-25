<template>
  <div class="app">
    <Header @addCard="addCard" />
    <Cards ref="cards" />
  </div>
</template>
<script>
export default {
  methods: {
    addCard() {
      this.$refs.cards.addCard();
    },
  },
};
</script>
