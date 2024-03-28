<template>
  <ul>
    <li class="border m-2 p-2 text-base cursor-pointer" v-for="card in cards" :key="card._id">{{ card.title }}</li>
  </ul>
</template>

<script>
export default {
  name: "CardList",
  props: {
    columnId: {
      type: String,
    }
  },
  data() {
    return {
      cards: []
    };
  },
  mounted() {
    this.fetchCards();
  },
  methods: {
    async fetchCards() {
      try {
        const response = await this.$axios.$get(`/card/column/${this.columnId}`);
        this.cards = response;
      } catch (error) {
        console.error("Error fetching cards:", error);
      }
    }
  }
 
};
</script>
