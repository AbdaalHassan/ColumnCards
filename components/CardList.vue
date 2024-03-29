<template>
  <div class="border p-4">
    <div class="flex flex-row justify-between items-center mb-4">
      <h1 class="text-xl font-semibold">Cards Lists</h1>
      <button
        @click="openCardModal(false)"
        class="rounded-2xl p-2 bg-blue-500 text-white hover:bg-blue-600 transition-colors duration-300"
      >
        Add Card
      </button>
    </div>

    <ul>
      <li
        class="border m-2 p-2 text-base cursor-pointer"
        v-for="card in cards"
        :key="card._id"
        @click="openCardModal(true, card)"
      >
        Title :{{ card.title }}
      </li>
    </ul>

    <Card
      @closeCardModal="closeCardModal"
      v-show="isCardModalVisible"
      @create-card="handleCreateCard"
      :selectedCard="selectedCard"
      @update-card="handleUpdateCard"
      :isUpdate="isUpdate"
    />
  </div>
</template>

<script>
import Card from "./Card.vue";
export default {
  name: "CardList",
  components: {
    Card,
  },
  props: {
    columnId: {
      type: String,
    },
  },
  data() {
    return {
      cards: [],
      isCardModalVisible: false,
      selectedCard: {},
      isUpdate: false,
    };
  },
  mounted() {
    this.fetchCards();
  },
  methods: {
    async fetchCards() {
      try {
        const response = await this.$axios.$get(
          `/card/column/${this.columnId}`
        );
        this.cards = response;
      } catch (error) {
        console.error("Error fetching cards:", error);
      }
    },

    closeCardModal() {
      this.isCardModalVisible = false;
    },
    openCardModal(isUpdate, card = null) {
      this.isCardModalVisible = true;
      this.selectedCard = card ? card : null;
      this.isUpdate = isUpdate;
    },

    handleCreateCard(value) {
      const requestBody = {
        column_id: this.columnId,
        title: value.title,
        description: value.description,
      };

      this.$axios
        .post("/card", requestBody)
        .then((response) => {
          console.log("Card created successfully:", response.data);
          this.fetchCards();
        })
        .catch((error) => {
          console.error("Error creating card:", error);
        });
    },
    handleUpdateCard(updatedCard) {
      const { _id, title, description } = updatedCard;
      const payload = {
        title,
        description,
      };
      this.$axios
        .put(`/card/${_id}`, payload)
        .then((response) => {
          console.log("Updated Card:", response.data);
          this.fetchCards();
        })
        .catch((error) => {
          console.error("Error updating card:", error);
        });
    },
  },
};
</script>
