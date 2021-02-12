<template>
  <div v-for="(result, index) in results" :key="index">
    <Card
      :caption="result.caption"
      :id="result.id"
      :name="result.name"
      :url="result.url"
    />
  </div>
</template>

<script>
import Card from "./components/Card.vue";

export default {
  name: "App",
  components: {
    Card
  },
  data() {
    return {
      results: []
    };
  },
  mounted() {
    fetch("https://xmeme-stream-backend.herokuapp.com/memes")
      .then(data => data.json())
      .then(data => {
        this.results = data;
        console.log(data);
      });
  }
};
</script>

<style></style>
