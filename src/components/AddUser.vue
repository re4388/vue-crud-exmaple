<template>
  <div>
    <b-form inline>
      <label class="mr-2" for="inline-form-input-name">Name</label>
      <b-input
        v-model="name"
        debounce="200"
        id="inline-form-input-name"
        class="mb-2 mr-sm-2 mb-sm-0"
        placeholder="Type name here..."
      ></b-input>
      <label class="mr-2" for="inline-form-input-name">Age</label>
      <b-input
        v-model="age"
        debounce="200"
        id="inline-form-input-name"
        class="mb-2 mr-sm-2 mb-sm-0"
        placeholder="Type age here.."
      ></b-input>
      <label class="mr-2" for="inline-form-input-name">Locate</label>
      <b-input
        v-model="locate"
        debounce="200"
        id="inline-form-input-name"
        class="mb-2 mr-sm-2 mb-sm-0"
        placeholder="Type Locate here..."
      ></b-input>
      <b-button @click="addUser" variant="primary">ADD</b-button>
    </b-form>
  </div>
</template>

<script>
// import axios from "axios";

export default {
  name: "AddUser",
  data() {
    return {
      name: "",
      age: 0,
      locate: ""
    };
  },
  props: {
    user: Object
  },

  methods: {
    addUser() {
      this.$emit("add-user", {
        name: this.name,
        age: this.age,
        loc: this.locate
      });
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
