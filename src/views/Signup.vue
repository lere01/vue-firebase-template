<template>
  <div class="sign-up">
    <p>Let's create a new account!</p>
    <input type="email" v-model="email" placeholder="Email" />
    <input type="password" v-model="password" placeholder="password" />
    <button @click="signUp">Sign Up</button>
    <span>
      Go back to
      <router-link to="/">login</router-link>
    </span>
  </div>
</template>

<script>
import firebase from "firebase";

export default {
  name: "SignUp",
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    signUp: function() {
      firebase
        .auth()
        .createUserWithEmailAndPassword(this.email, this.password)
        .then(
          () => {
            alert("You have successfully registered");
            this.$router.replace("home");
          },
          function(err) {
            alert("An error occured: " + err.message);
          }
        );
    }
  }
};
</script>

<style scoped>
.sign-up {
  margin-top: 40px;
}

input {
  margin: 10px 0;
  width: 20%;
  padding: 15px;
}

button {
  margin-top: 10px;
  width: 10%;
  cursor: pointer;
}

span {
  display: block;
  margin-top: 20px;
  font-size: 11px;
}
</style>
