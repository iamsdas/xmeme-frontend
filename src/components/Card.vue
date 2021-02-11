<template>
  <div>
    <div>Name: {{ name }}</div>
    <div>URL: {{ url }}</div>
    <div>caption: {{ caption }}</div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    name: String,
    url: String,
    caption: String
  }
};
</script>

<style scoped></style>>
