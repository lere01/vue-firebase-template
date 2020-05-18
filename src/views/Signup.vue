<template>
  <div class="sign-up">
    <p>Register An Account!</p>
    <input type="email" v-model="email" placeholder="Email" /><br />
    <input type="password" v-model="password" placeholder="Password" /><br />
    <input
      type="password"
      v-model="cpassword"
      placeholder="Confirm Password"
    /><br />
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
      password: "",
      cpassword: ""
    };
  },
  methods: {
    signUp: function() {
      if (this.password === this.cpassword) {
        firebase
          .auth()
          .createUserWithEmailAndPassword(this.email, this.password)
          .then(
            () => {
              alert(
                "You have successfully registered. Please login in with your credentials."
              );
              this.$router.replace("login");
            },
            function(err) {
              alert("An error occured: " + err.message);
            }
          );
      } else alert("You have entered different passwords");
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
