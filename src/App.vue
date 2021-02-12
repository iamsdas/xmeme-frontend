<template>
  <button class="btn btn-primary" @click="updateList()">update</button>
  <new-meme @update="updateList()" />
  <div class="container-fluid">
    <div
      class="row row-cols-1 justify-content-center"
      v-for="(result, index) in results"
      :key="index"
    >
      <Card
        :caption="result.caption"
        :id="result.id"
        :name="result.name"
        :url="result.url"
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
      results: []
    };
  },
  methods: {
    updateList() {
      fetch("https://xmeme-stream-backend.herokuapp.com/memes")
        .then(data => data.json())
        .then(data => {
          this.results = data;
        });
    }
  },
  mounted() {
    this.updateList();
  }
};
</script>

<style></style>
