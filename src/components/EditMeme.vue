<template>
  <!-- Button trigger modal -->
  <button
    type="button"
    class="btn btn-sm"
    data-bs-toggle="modal"
    :data-bs-target="modalIdHash"
  >
    <i class="bi bi-pencil-fill"></i>
  </button>
  <!-- Modal -->
  <div
    class="modal fade"
    :id="modalId"
    tabindex="-1"
    aria-labelledby="memeModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <!-- Modal Header -->
        <div class="modal-header">
          <h5 class="modal-title" id="memeModalLabel">Add new meme</h5>
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
              class="btn btn-outline-secondary"
              data-bs-dismiss="modal"
            >
              Close
            </button>
            <button
              type="button"
              class="btn btn-outline-success"
              data-bs-dismiss="modal"
              @click="editMeme()"
            >
              Update
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
  name: "EditMeme",
  data() {
    return {
      url: this.origin_url,
      caption: this.origin_caption,
      id: this.origin_id
    };
  },
  props: {
    origin_url: {
      type: String,
      default: ""
    },
    origin_caption: {
      type: String,
      default: ""
    },
    origin_id: {
      type: Number
    }
  },
  emits: ["update"],
  computed: {
    body() {
      return { url: this.url, caption: this.caption };
    },
    modalId() {
      return "modal" + `${this.id}`;
    },
    modalIdHash() {
      return "#modal" + `${this.id}`;
    }
  },
  methods: {
    editMeme() {
      axios
        .patch(
          "https://xmeme-stream-backend.herokuapp.com/memes/" + `${this.id}`,
          this.body
        )
        .then(() => {
          this.$emit("update");
        });
    }
  }
};
</script>
