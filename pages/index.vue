<template>
  <div class="bg-gray-300 h-screen">
    <!-- listen the header event and call a method -->
    <Header @column-created="handleColumnCreated" />

    <!-- It uniquely identifies each element/component in a list -->
    <!-- Vue watches the key prop for changes. If it changes, Vue re-renders the associated component or DOM element -->
    <!-- Add column and emit event, Listen in index, :key change tell the vue to update the element but here component in my case -->
    <Columns :key="refreshColumns" />
  </div>
</template>

<script>
import Headers from "../components/Header.vue";
import Columns from "../components/Columns.vue";

export default {
  name: "IndexPage",
  data() {
    return {
      refreshColumns: false,
    };
  },
  comments: {
    Headers,
    Columns,
  },
  methods: {
    handleColumnCreated() {
      this.refreshColumns = !this.refreshColumns;
    },
  },
};
</script>
