<template>
  <div>
    <h2>All Columns</h2>
    <ul>
      <li v-for="column in columns" :key="column._id">{{ column.title }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Columns",
  data() {
    return {
      columns: [],
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
  },
};
</script>
