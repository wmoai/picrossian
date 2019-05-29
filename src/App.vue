<template>
  <div id="app">
    <Picross
      :columns="[[3], [0], [1, 1], [0], [0], [0], [0], [0]]"
      :rows="[[1, 1], [1], [1, 1], [0], [0], [0], [0], [0]]"
    />
  </div>
</template>

<script>
import Picross from './components/Picross.vue';

export default {
  name: 'app',
  components: {
    Picross,
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
