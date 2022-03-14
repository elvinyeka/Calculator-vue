<template>
  <div>
    <CalculatorView />
  </div>
</template>

<script>
import CalculatorView from "./components/CalculatorView.vue";
export default {
  name: "App",
  components: {
    CalculatorView,
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
  margin-top: 35px;
}
</style>
