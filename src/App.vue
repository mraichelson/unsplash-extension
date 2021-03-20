<template>
  <div id="app">{{ txt }}</div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      txt: 'hello from vue',
    }
  },
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
