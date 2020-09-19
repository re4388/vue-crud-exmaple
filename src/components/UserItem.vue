<template>
  <div>
    <div class="d-flex">
      <b-card
        :title="user.name"
        :img-src="user.link"
        img-alt="Image"
        img-top
        tag="article"
        style="max-width: 15rem;"
        class="mb-2"
      >
        <b-card-text>
          {{ user.name }} | {{ user.age }} | {{ user.loc }}
        </b-card-text>

        <b-button
          type="button"
          class="btn btn-info btn-sm m-2"
          @click="showUpdateModal = true"
          >Update</b-button
        >
        <update-user
          v-if="showUpdateModal"
          :user="user"
          @update-user="update"
          @close="closeModal()"
        />

        <b-button type="button" class="btn btn-danger btn-sm" @click="remove()">
          Delete</b-button
        >
      </b-card>
    </div>
  </div>
</template>

<script>
import UpdateUser from "./UpdateUser";

export default {
  name: "UserItem",
  components: {
    UpdateUser
  },
  data() {
    return {
      imgsrc: "https://picsum.photos/600/300/?image=25",
      showUpdateModal: false
    };
  },
  props: {
    user: Object,
    imglinks: Object
  },
  methods: {
    remove() {
      this.$emit("remove-user", {
        ...this.user
      });
    },

    update(data) {
      this.$emit("update-user", {
        ...data
      });
      this.showUpdateModal = false;
    },
    closeModal() {
      this.showUpdateModal = false;
    }
  },
  mounted() {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
