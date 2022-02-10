<template>
  <div>
    <div v-if="loading">Loading</div>
    <div v-else>
      <h2>The api says:</h2>
      <p>{{ message }}</p>
      <h2>It also knows about</h2>
      <p>{{ meta }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loading: true,
      message: "",
      meta: "",
    };
  },
  methods: {
    async fetch() {
      try {
        console.log("fetching");
        console.log(import.meta.env);
        const response = await fetch(import.meta.env.VITE_API_URL);
        const results = await response.json();
        this.message = results.message;
        this.meta = results.meta;
        this.loading = false;
      } catch (err) {
        if (err.response) {
          console.log("Server Error:", err);
        } else if (err.request) {
          console.log("Network Error:", err);
        } else {
          console.log("Client Error:", err);
        }
      }
    },
  },
  mounted() {
    console.log("mounted");
    this.fetch();
  },
};
</script>
