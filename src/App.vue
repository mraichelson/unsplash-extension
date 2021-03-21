<template>
  <div id="app">
    <form action="#">
      <label for="width">Width</label>
      <input
        type="number"
        id="width"
        name="width"
        v-model="width"
        min="1"
        required
      />
      <br />
      <label for="height">Height</label>
      <input
        type="number"
        id="height"
        name="height"
        v-model="height"
        min="1"
        required
      />
      <br />
      <label for="greyscale">
        <input
          type="checkbox"
          id="greyscale"
          name="greyscale"
          v-model="greyscale"
        />
        Greyscale
      </label>
      <details>
        <summary>Advanced options</summary>
        <div>Lorem ipsum dolor sit amet.</div>
      </details>
    </form>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      width: 320,
      height: 240,
      greyscale: false
    }
  }
}
</script>

<style lang="scss">
$light: #eef;
$dark: #113;

html,
body {
  background-color: $light;
  color: $dark;
  padding: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
// #app {}
label {
  display: block;
  margin: 1rem 0 0.25rem;
}
details {
  summary {
    cursor: pointer;
  }
}
</style>
