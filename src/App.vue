<template>
  <play-area/>
</template>

<script>
import PlayArea from './components/PlayArea.vue';
export default {
  name: "App",
  components: {
    PlayArea,
    },
  data() {
    return {};
  },
  created() {
    var haystack = ["11", "00", "22", "12"];
    var  needle = ["11", "00", "22"];
    var result = needle.every((i) => haystack.includes(i));
    console.log(result);
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  /* color: #2c3e50; */
  color: white;
  margin-top: 60px;
}
</style>
