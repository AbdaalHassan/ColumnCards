<template>
  <div
    class="flex justify-center items-center h-screen fixed top-0 left-0 right-0 bottom-0 bg-gray-900 bg-opacity-50 z-50"
  >
    <div class="bg-white rounded-lg shadow-lg p-6">
      <!-- Modal Header -->
      <div class="flex justify-between items-center mb-4 p-2">
        <h1 class="text-lg font-bold">{{ modalHeader }}</h1>
        <button
          @click="closeModal"
          class="text-gray-500 hover:text-gray-700 focus:outline-none"
        >
          <svg
            class="w-6 h-6"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M6 18L18 6M6 6l12 12"
            ></path>
          </svg>
        </button>
      </div>

      <!-- Modal Body -->
      <div class="mb-4 mt-4">
        <label
          class="block text-gray-700 text-sm font-bold mb-2"
          for="username"
        >
          {{ modalLabel }}
        </label>

        <!-- v-model creates a link between the  (value attribute) and data value in the Vue instance. -->
        <!--  It automatically picks the correct way to update the element based on the input type. -->
        <input
          class="shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          type="text"
          v-model="inputValue"
        />
      </div>

      <div class="flex justify-end mt-8">
        <button
          @click="createItem"
          class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600"
        >
          Create
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  data() {
    return {
      inputValue: "",
    };
  },
  // Props for receiving values
  // String , vue js do type validation that these props only receive string values
  props: {
    modalHeader: String,
    modalLabel: String,
  },
  // methods
  // this refer to current component
  // this.emit it emits a custom event that can be listened in parent component where it calls
  methods: {
    closeModal() {
      this.$emit("close");
    },
    // when click on create button emit an event with its name and value in payload
    createItem() {
      this.$emit("create-item", this.inputValue);
      this.inputValue = "";
    },
  },
};
</script>
