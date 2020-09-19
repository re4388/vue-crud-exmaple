<template>
  <div>
    <transition name="modal">
      <div class="modal-mask">
        <div class="modal-wrapper">
          <div class="modal-container">
            <div class="modal-header"></div>
            <h3>Update Form</h3>
            <div class="modal-body"></div>
            <b-form inline class="mb-4">
              <div>
                <label class="mr-2" for="inline-form-input-name">Name</label>
                <b-input
                  v-model="name"
                  debounce="200"
                  id="inline-form-input-name"
                  class="mb-2 mr-sm-2 mb-sm-0"
                  placeholder="Type name here..."
                ></b-input>
              </div>
              <br />
              <div>
                <label class="mr-2" for="inline-form-input-name">Age</label>
                <b-input
                  v-model="age"
                  debounce="200"
                  id="inline-form-input-name"
                  class="mb-2 mr-sm-2 mb-sm-0"
                  placeholder="Type age here.."
                ></b-input>
              </div>
              <br />
              <div>
                <label class="mr-2" for="inline-form-input-name">Locate</label>
                <b-input
                  v-model="locate"
                  debounce="200"
                  id="inline-form-input-name"
                  class="mb-2 mr-sm-2 mb-sm-0"
                  placeholder="Type Locate here..."
                ></b-input>
              </div>
            </b-form>

            <div class="modal-footer">
              <b-button variant="primary" @click="updateUser">Update</b-button>
              <b-button variant="danger" @click="$emit('close')"
                >Close</b-button
              >
            </div>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "UserItem",
  data() {
    return {
      name: this.user.name,
      age: this.user.age,
      locate: this.user.loc,
      id: this.user._id
    };
  },
  props: {
    user: Object
  },
  methods: {
    updateUser() {
      this.$emit("update-user", {
        name: this.name,
        age: this.age,
        loc: this.locate,
        id: this.id
      });
    }
    // remove() {
    //   this.$emit("remove-user", {
    //     ...this.user
    //   });
    // },
    // update() {
    //   this.$emit("update-user", {
    //     ...this.user
    //   });
    // }
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

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

/* .modal-body {
  margin: 20px 0;
} */

/* .modal-default-button {
  float: right;
} */

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>
