<template>
  <div class="col-xs-10 col-sm-8 col-md-6 col-lg-4">
    <div class="card">
      <div class="card-header justify-content-between d-flex">
        <div>{{ name }}</div>
        <edit-meme
          :origin_id="id"
          :origin_url="url"
          :origin_caption="caption"
          @update="update()"
        />
      </div>
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
import EditMeme from "./EditMeme.vue";
export default {
  name: "Card",
  components: {
    EditMeme
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
      event.target.src =
        "https://breakthrough.org/wp-content/uploads/2018/10/default-placeholder-image.png";
    },
    update() {
      this.$emit("update");
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
.btn-sm {
  padding: 0;
  margin: 0;
}
</style>
