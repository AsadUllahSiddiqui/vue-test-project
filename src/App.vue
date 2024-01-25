<template>
  <!-- <HeaderComp /> -->
  <PetRegistrationForm />
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import PetRegistrationForm from "./components/PetRegistrationForm.vue";
// import HeaderComp from "./components/Header.vue";

export default {
  name: "App",
  components: {
    // HeaderComp,
    PetRegistrationForm,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
  background-color: #e0dfdf;
}
</style>
