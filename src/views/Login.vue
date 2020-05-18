<template>
  <div class="login">
    <h3>Sign In</h3>
    <input type="email" v-model="email" placeholder="Email" />
    <br />
    <input type="password" v-model="password" placeholder="Password" />
    <br />
    <button @click="signin">Login</button>
    <p>
      You don't have an account yet? You can
      <router-link to="/sign-up">Sign up</router-link>
    </p>
  </div>
</template>

<script>
import firebase from "firebase";

export default {
  name: "Login",
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    signin: function() {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
        .then(
          () => {
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
.login {
  margin-top: 40px;
}

input {
  margin: 10px 0;
  width: 20%;
  padding: 15px;
}

p {
  margin-top: 40px;
  font-size: 13px;
}

p a {
  text-decoration: underline;
  cursor: pointer;
}
</style>
