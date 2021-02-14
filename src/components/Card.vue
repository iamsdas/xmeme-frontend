<template>
  <div class="col-12 col-sm-8 col-md-6 col-lg-4">
    <div class="card">
      <!-- header  -->
      <div class="card-header justify-content-between d-flex">
        <div>{{ name }}</div>
        <edit-meme
          :origin_id="id"
          :origin_url="url"
          :origin_caption="caption"
          @update="update()"
        />
      </div>
      <!-- image  -->
      <div class="d-flex justify-content-center">
        <img
          class="img-fluid"
          :src="src"
          loading="lazy"
          @error="showAltImage"
        />
      </div>
      <!-- caption -->
      <div class="card-body">
        <p class="card-text">{{ caption }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import EditMeme from "./EditMeme.vue";
export default {
  name: "Card",
  components: {
    EditMeme
  },
  data() {
    return {
      placeholder: require("../assets/placeholder.png"),
      loading: require("../assets/loading.gif"),
      src: ""
    };
  },
  emits: ["update"],
  props: {
    name: String,
    url: String,
    caption: String,
    id: Number
  },
  methods: {
    showAltImage(event) {
      event.target.src = this.src;
    },
    update() {
      this.$emit("update");
    }
  },
  watch: {
    url: {
      immediate: true,
      handler(newUrl) {
        var newImage = new Image();
        this.src = this.loading;
        newImage.src = newUrl;
        newImage.onload = () => {
          this.src = newUrl;
        };
        newImage.onerror = () => {
          this.src = this.placeholder;
        };
      }
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
