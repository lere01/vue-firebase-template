<template>
  <div class="home">
    <fieldset>
      <input type="number" placeholder="loan amount" v-model="loan" />
      <input type="number" placeholder="period" v-model="time" />
      <input
        type="number"
        placeholder="% interest rate per year"
        v-model="rate"
      />
      <span id="result"></span>
      <button @click="payback">Calculate Payback</button>
    </fieldset>
    <button @click="signOut">Sign Out</button>
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
