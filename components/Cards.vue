<template>
  <div class="cards">
    <Card
      v-for="(item, i) in items"
      :key="i"
      @select="selected = item"
      :class="{ active: selected === item }"
      :item="item"
      @close="close"
    />
  </div>
</template>
<script>
export default {
  data: () => ({
    items: [],
    selected: null,
  }),
  methods: {
    addCard() {
      const newItem = {
        id: Math.round(new Date().getTime() / 1000),
        value: 100,
      };
      this.items.push(newItem);
    },
    close() {
      this.selected = null;
    },
  },
};
</script>
