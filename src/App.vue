<template>
  <div id="app">
    <p style="font-weight: 800; font-size: 24px;">So you wanna rat labs</p>
    <img alt="labs" src="./assets/LAB.gif">
    <ClockTimer></ClockTimer>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import ClockTimer from './components/ClockTimer.vue';

export default Vue.extend({
  name: 'App',
  components: {
    ClockTimer
  }
});
</script>

<style>
html {
  background-color: black;
  font-family: Arial, Helvetica, sans-serif
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
