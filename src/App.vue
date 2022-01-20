<template>
    <div id="app">
        <Calculator />
    </div>
</template>

<script>
import Calculator from "./components/Calculator.vue";

export default {
    name: "app",
    components: {
        Calculator,
    },
};
</script>

<style>
#app {
  color: #fae1df;
  font-family: 'Anton', sans-serif;
  font-weight: bold;
  text-align: center;
  margin-top: 60px;
}
</style>
