<template>
  <div
    class="flex justify-center items-center h-screen fixed top-0 left-0 right-0 bottom-0 bg-gray-900 bg-opacity-50 z-50"
  >
    <div class="bg-white rounded-lg shadow-lg p-6">
      <div class="flex justify-between items-center mb-4 p-2">
        <h1 class="text-lg font-bold">
          {{ isUpdate ? "Update Card" : "Create Card" }}
        </h1>
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

      <div class="mb-4 mt-4">
        <label class="block text-gray-700 text-sm font-bold mb-2">Title</label>
        <input
          class="shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          type="text"
          v-model="title"
        />
      </div>

      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2"
          >Description</label
        >
        <textarea
          class="shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          rows="4"
          v-model="description"
        ></textarea>
      </div>

      <div class="flex justify-end mt-8">
        <button
          v-if="isUpdate"
          @click="updateCard"
          class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600"
        >
          Update
        </button>
        <button
          v-else
          @click="createCard"
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
  name: "Card",
  props: {
    selectedCard: {
      type: Object,
    },
    isUpdate: {
      type: Boolean,
    },
  },
  // Below is vue configuration option in vue instance
  // const app = Vue.createApp({
  //   data() {
  //     ...
  //   },
  //   watch: {
  //     ...
  //   },
  //   computed: {
  //     ...
  //   },
  //   methods: {
  //     ...
  //   }
  // })

  // the watch option allows you to perform side effects in response to changes
  //  in data properties, computed properties, or props.

  // Property to Watch:selectedCard
  // This is the property you want to observe for changes. It could be a data property,
  //  a computed property, or a prop passed from a parent component.

  // The handler function is called whenever the watched property changes.
  // It receives two arguments: newValue (the new value of the watched property)
  // and oldValue (the previous value of the watched property).
  // Inside the handler function, you can define custom logic to execute in response to the change.

  // If immediate is set to true, the handler function will be called immediately after the watcher is created, with the current value of the watched property.
  // This is useful when you want to perform an initial action based on the current value of the watched property when the component is first mounted.

  watch: {
    selectedCard: {
      handler(newValue) {
        if (this.isUpdate) {
          this.title = newValue ? newValue.title : "";
          this.description = newValue ? newValue.description : "";
        } else {
          this.title = "";
          this.description = "";
        }
      },
      immediate: true,
    },
  },

  data() {
    return {
      title: "",
      description: "",
    };
  },
  methods: {
    closeModal() {
      this.$emit("closeCardModal");
    },
    createCard() {
      this.$emit("create-card", {
        title: this.title,
        description: this.description,
      });
      this.title = "";
      this.description = "";
      this.closeModal();
    },
    updateCard() {
      this.$emit("update-card", {
        ...this.selectedCard,
        title: this.title,
        description: this.description,
      });
      this.closeModal();
    },
  },
};
</script>

