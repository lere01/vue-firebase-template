<template>
  <div class="home">
    <div class="nav">
      <button id="signout" @click="signOut">Sign Out</button>
    </div>

    <fieldset>
      <input type="text" placeholder="loan amount" v-model="loan" /><br />
      <input type="text" placeholder="period" v-model="time" /><br />
      <input
        type="text"
        placeholder="% interest rate per year"
        v-model="rate"
      /><br />
      <span id="result"></span>
      <button @click="payback">Calculate Payback</button>
    </fieldset>
  </div>
</template>

<script>
// @ is an alias to /src
import firebase from "firebase";

export default {
  name: "Home",
  components: {},
  data() {
    return {
      loan: "",
      time: "",
      rate: "",
      payment: ""
    };
  },
  methods: {
    signOut: function() {
      firebase
        .auth()
        .signOut()
        .then(() => {
          this.$router.replace("login");
        });
    },
    payback: function() {
      this.payment = this.loan + this.loan * this.time * (this.rate / 100);

      let result = document.querySelector("#result");
      result.textContent = this.payment;
    }
  }
};
</script>

<style scoped>
.home {
  margin: 100px auto;
  max-width: 500px;
  min-width: 300px;
}

.nav {
  display: flex;
  justify-content: flex-end;
  margin-bottom: 10px;
}

fieldset {
  box-shadow: 2px 3px 5px rgba(49, 45, 45, 0.6);
  box-sizing: border-box;
  border: none;
}

input {
  margin: 10px 0;
  width: 50%;
  padding: 15px;
  padding-bottom: 5px;
  text-align: left;
  border: none;
  border-bottom: 1px solid #808080;
  font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
  font-size: 14px;
}

button {
  margin-top: 10px;
  width: 100px;
  border-radius: 5px;
  cursor: pointer;
  padding: 10px;
}

span {
  display: block;
  margin-top: 20px;
  font-size: 24px;
}
</style>
