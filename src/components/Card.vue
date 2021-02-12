<template>
  <div class="col-sm-5">
    <div class="card">
      <div class="card-header">{{ name }}</div>
      <div>
        <img class="img-fluid" :src="url" @error="showAltImage" />
      </div>
      <div class="card-body">
        <p class="card-text">{{ caption }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    name: String,
    url: String,
    caption: String,
    id: Number
  },
  methods: {
    showAltImage(event) {
      event.target.src =
        "https://breakthrough.org/wp-content/uploads/2018/10/default-placeholder-image.png";
    }
  }
};
</script>

<style scoped>
.card {
  margin: 5px 0px;
}
.card-header {
  text-transform: capitalize;
}
</style>
