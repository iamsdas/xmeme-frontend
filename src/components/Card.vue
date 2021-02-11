<template>
  <div class="container-fluid">
    <div>Name: {{ name }}</div>
    <div>
      <img :src="url" @error="showAltImage" />
    </div>
    <div>caption: {{ caption }}</div>
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

<style scoped></style>>
