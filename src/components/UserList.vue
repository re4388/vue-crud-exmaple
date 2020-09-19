<template>
  <div>
    <h2>{{ msg }}</h2>
    <add-user @add-user="addUser"></add-user>
    <div>
      <ul class="d-flex justify-content-center flex-wrap bd-highlight m-3">
        <li v-for="user in userAndLink" :key="user.id" :imglinks="imgLink">
          <user-item
            :user="user"
            @remove-user="removeUser"
            @update-user="updateUser"
          >
          </user-item>
        </li>
      </ul>
    </div>

    <!-- style play ground -->
    <!-- <div class="d-flex flex-row bd-highlight mb-3">
      <div class="p-2 bd-highlight">Flex item 1</div>
      <div class="p-2 bd-highlight">Flex item 2</div>
      <div class="p-2 bd-highlight">Flex item 3</div>
    </div>
    <div class="d-flex flex-row-reverse bd-highlight">
      <div class="p-2 bd-highlight">Flex item 1</div>
      <div class="p-2 bd-highlight">Flex item 2</div>
      <div class="p-2 bd-highlight">Flex item 3</div>
    </div> -->
  </div>
</template>

<script>
import axios from "axios";
import UserItem from "./UserItem";
import AddUser from "./AddUser";
import imgSrcLink from "../assets/imgsrc";

export default {
  components: {
    UserItem,
    AddUser
  },
  name: "HelloWorld",
  data() {
    return {
      users: [],
      imgLink: imgSrcLink
    };
  },
  props: {
    msg: String
  },

  computed: {
    userAndLink() {
      let linkArr = this.imgLink.data;
      let count = 0;
      let newUser = this.users;
      newUser.map(item => {
        item["link"] = linkArr[count];
        count++;
      });

      return newUser;
    }
  },

  mounted() {
    this.getUser();
  },

  methods: {
    getUser() {
      axios.get("http://localhost:3000/user").then(response => {
        console.log(response.data);
        this.users = response.data;
      });
    },
    addUser(newUser) {
      axios.post("http://localhost:3000/user", newUser).then(response => {
        console.log(response);
        this.getUser();
      });
    },
    removeUser(user) {
      let id = user._id;
      axios.delete("http://localhost:3000/user/" + id).then(response => {
        console.log(response);

        // I think the realtime DB (nosql)have some properties I don't know
        // the response is done but the db have not yet complete process..
        // I delay 2 sec to let it work, but UX will be lower
        setTimeout(() => {
          this.getUser();
          console.log(this.users);
        }, 1000);
      });
    },
    updateUser(user) {
      let id = user.id;
      let newUser = user;
      console.log(`id`, id);
      console.log(`newUser`, newUser);
      axios.put("http://localhost:3000/user/" + id, newUser).then(response => {
        console.log(response);
        setTimeout(() => {
          this.getUser();
        }, 1000);

        // that.$nextTick(function() {
        //   this.getUser(); //输出：修改后的值
        //   this.$forceUpdate();
        // });
      });
    }
  }
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
  display: inline;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
