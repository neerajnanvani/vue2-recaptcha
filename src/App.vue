<template>
  <div id="app">
    <header>
      <img alt="Vue logo" src="./assets/logo.png" width="25%" />
    </header>
    <button @click="openSimplert">Open Simplert with reCAPTCHA.</button>
    <simplert :useRadius="true" :useIcon="false" ref="simplert">
      <template v-slot:header>
        <vue-lottie-player
          name="protectionShield"
          loop
          path="https://assets2.lottiefiles.com/packages/lf20_kQW6MG.json"
          style="margin: 0 auto"
        />
      </template>
      <vue-recaptcha
        ref="recaptcha"
        sitekey="6LeIxAcTAAAAAJcZVRqyHh71UMIEGNQ_MXjiZKhI"
        style="
          display: flex;
          justify-content: center;
          height: 78px;
          margin-top: 10px;
        "
        @verify="verify"
        @expired="expired"
      ></vue-recaptcha>
    </simplert>
  </div>
</template>

<script>
import Simplert from "./components/Simplert";
import VueRecaptcha from "vue-recaptcha";
import VueLottiePlayer from "vue-lottie-player";

export default {
  name: "App",
  components: {
    Simplert,
    VueRecaptcha,
    VueLottiePlayer,
  },
  methods: {
    openSimplert(id) {
      this.$refs.simplert.openSimplert({
        message: "Please check the following:",
        customCloseBtnText: "I'm a robot!",
        disableOverlayClick: true,
      });
    },
    verify() {
      setTimeout(() => {
        this.$refs.simplert.justCloseSimplert();
        this.$refs.recaptcha.reset();
      }, 1200);
    },
    expired() {
      this.$refs.recaptcha.reset();
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

a,
button {
  color: #4fc08d;
}

button {
  background: none;
  border: solid 1px;
  border-radius: 2em;
  font: inherit;
  padding: 0.75em 2em;
}
</style>
