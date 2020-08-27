<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
    <!-- <HelloWorld msg="This is Vue 2 Component" /> -->
    <!-- <Test   msg="This is Vue 3 Component" /> -->
    <Calendar />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Test from "./components/Test.vue";
import Calendar from "./components/Calendar.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    Test,
    Calendar,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
