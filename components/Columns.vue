<template>
  <div class="m-4">
    <div class="flex flex-wrap">
      <div
        class="border bg-white m-2 w-96 p-4"
        v-for="column in columns"
        :key="column._id"
      >
        <div class="flex flex-col justify-between border bg-white p-2 mt-4">
          <!-- Header section with title and buttons -->
          <div class="flex items-center justify-between mb-4">
            <h2 class="text-lg font-semibold">{{ column.title }}</h2>
            <div class="flex space-x-2">
              <button
                @click="openCardModal"
                class="rounded-full p-2 bg-blue-500 text-white hover:bg-blue-600 transition-colors duration-300"
              >
                Add Card
              </button>
              <button
                class="rounded-full p-2 bg-red-500 text-white hover:bg-red-600 transition-colors duration-300"
              >
                Delete Column
              </button>
            </div>
          </div>

          <!-- Body section with list -->
          <div>
            <ul>
              <li>1</li>
              <li>2</li>
              <li>3</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
    <Card
      v-show="isCardModalVisible"
      @closeCardModal="closeCardModal"
      @create-card="handleCreateCard"
    />
  </div>
</template>




<script>
import Card from "./Card.vue";
export default {
  name: "Columns",
  components: {
    Card,
  },

  data() {
    return {
      columns: [],
      isCardModalVisible: false,
    };
  },
  mounted() {
    this.fetchColumns();
  },
  methods: {
    async fetchColumns() {
      try {
        const response = await this.$axios.$get("/column");
        this.columns = response;
      } catch (error) {
        console.error("Error fetching columns:", error);
      }
    },

    openCardModal() {
      this.isCardModalVisible = true;
    },
    closeCardModal() {
      this.isCardModalVisible = false;
    },

    handleCreateCard(value) {
      console.log(value);
    },
  },
};
</script>
