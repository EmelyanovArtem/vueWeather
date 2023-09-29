<template>
  <my_posts></my_posts>
</template>

<script>
import my_posts from './components/postsInMain.vue'

export default {
  name: 'App',
  components: {
    my_posts,
  }
}
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color:rgb(160, 93, 223);
  margin-top: 60px;
}

.body {
  background-color: rgb(43, 43, 43);
}
</style>
