<template>
  <!-- Button trigger modal -->
  <button
    type="button"
    class="btn btn-primary"
    data-bs-toggle="modal"
    data-bs-target="#exampleModal"
  >
    Add
  </button>

  <!-- Modal -->
  <div
    class="modal fade"
    id="exampleModal"
    tabindex="-1"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <form>
          <div class="modal-body">
            <label for="name">Name: </label>
            <input type="text" v-model="name" />
            <br />
            <label for="url">URL: </label>
            <input type="text" v-model="url" />
            <br />
            <label for="caption">Caption:</label>
            <input type="text" v-model="caption" />
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Close
            </button>
            <button type="button" class="btn btn-primary" @click="addNewMeme()">
              Add
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "NewMeme",
  data() {
    return {
      name: "",
      url: "",
      caption: ""
    };
  },
  emits: ["update"],
  computed: {
    body() {
      return { name: this.name, url: this.url, caption: this.caption };
    }
  },
  methods: {
    addNewMeme() {
      axios
        .post("https://xmeme-stream-backend.herokuapp.com/memes", this.body)
        .then(() => {
          this.$emit("update");
        });
    }
  }
};
</script>
