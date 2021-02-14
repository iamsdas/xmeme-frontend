<template>
  <!-- Navbar -->
  <nav class="navbar navbar-expand-lg navbar-light bg-light sticky-top">
    <div class="container-fluid">
      <div class="navbar-header">
        <a class="navbar-brand" href="/">XMeme</a>
      </div>
      <form class="d-flex gap-1">
        <button class="btn btn-outline-primary" @click="updateList()">
          Refresh
        </button>
        <new-meme @update="updateList()" />
      </form>
    </div>
  </nav>
  <!-- Body -->
  <div class="container-fluid">
    <!-- Loading Spinner -->
    <div v-if="loading" class="d-flex justify-content-center">
      <div class="spinner-border m-5 text-primary" role="status">
        <span class="visually-hidden">Loading...</span>
      </div>
    </div>
    <!-- Cards List -->
    <div
      class="row row-cols-1 justify-content-center"
      v-for="(result, index) in results"
      :key="index"
    >
      <!-- Card -->
      <Card
        :caption="result.caption"
        :id="result.id"
        :name="result.name"
        :url="result.url"
        @update="updateList()"
      />
    </div>
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import NewMeme from "./components/NewMeme.vue";

export default {
  name: "App",
  components: {
    Card,
    NewMeme
  },
  data() {
    return {
      results: [],
      loading: false
    };
  },
  methods: {
    updateList() {
      this.loading = true;
      fetch("https://xmeme-stream-backend.herokuapp.com/memes")
        .then(data => data.json())
        .then(data => {
          this.results = data;
          this.loading = false;
        });
    }
  },
  mounted() {
    this.updateList();
  }
};
</script>

<style>
.modal-backdrop {
  position: unset !important;
}
</style>
