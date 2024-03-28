<template>
  <!--  data() where is component states -->
  <div>
    <header class="flex justify-around items-center px-4 py-2 bg-indigo-400">
      <h1 class="text-lg font-bold text-white">Column Cards</h1>
      <button
        class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600"
        @click="createColumn"
      >
        Create Column
      </button>
    </header>
    <!-- Props Name (modalHeader) & (modalLabel)  -->
    <!-- values (header) & (label)  -->
    <!-- v-bind is a way to dynamically bind data from your Vue instance to HTML attributes or props in custom components -->
    <!-- <a v-bind:href="url">Click me</a>  -->

    <!-- v-show hide an element if the condition is false -->
    <!-- @close event listen here and then update the state -->
    <Modal
      v-show="isModalVisible"
      @close="closeModal"
      @create-item="handleCreateItem"
      :modalHeader="header"
      :modalLabel="label"
    />
  </div>
</template>

<script>
import Modal from "../components/Modal.vue";

export default {
  name: "Header",
  components: {
    Modal,
  },
  //   data is a function that return the object and this object contain the data properties of a component
  data() {
    return {
      header: "Create a new Column",
      label: "Column Title",
      isModalVisible: false,
    };
  },
  // methods
  methods: {
    createColumn() {
      this.isModalVisible = true;
    },

    closeModal() {
      this.isModalVisible = false;
    },

    // value parameter comes from the event value in 2nd argument
    async handleCreateItem(value) {
      try {
        const response = await this.$axios.$post("/column", { title: value });
        console.log(response.data);
        this.isModalVisible = false;
        // notify the parent component that column is created
        // listen this event into parent 
        this.$emit("column-created");
      } catch (error) {
        console.error("Error creating column:", error);
      }
    },
  },
};
</script>

