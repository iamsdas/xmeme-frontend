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
    fetch("http://54.211.242.231:8081/meme")
      .then(data => data.json())
      .then(data => {
        this.results = data;
        console.log(data);
      });
  }
};
</script>

<style></style>
