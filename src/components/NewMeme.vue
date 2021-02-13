<template>
  <!-- Button trigger modal -->
  <button
    type="button"
    class="btn btn-outline-primary"
    data-bs-toggle="modal"
    data-bs-target="#addModal"
  >
    Add Meme
  </button>
  <!-- Modal -->
  <div
    class="modal fade"
    id="addModal"
    tabindex="-1"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <!-- Modal Header -->
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Add new meme</h5>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <form>
          <!-- Modal Body (Form) -->
          <div class="modal-body">
            <label class="form-label" for="name">Name: </label>
            <input class="form-control" type="text" v-model="name" />
            <br />
            <label class="form-label" for="url">URL: </label>
            <input class="form-control" type="text" v-model="url" />
            <br />
            <label class="form-label" for="caption">Caption:</label>
            <input class="form-control" type="text" v-model="caption" />
          </div>
          <!-- Modal Footer (Buttons) -->
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Close
            </button>
            <button
              type="button"
              class="btn btn-outline-success"
              @click="addNewMeme()"
            >
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
