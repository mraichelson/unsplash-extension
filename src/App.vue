<template>
  <div id="app">
    <h1>Lorem Picsum</h1>
    <form action="#" @submit.prevent="formSubmit">
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
      <label for="grayscale">
        <input
          type="checkbox"
          id="grayscale"
          name="grayscale"
          v-model="grayscale"
        />
        Grayscale
      </label>
      <details>
        <summary>Advanced options</summary>
        <div>Lorem ipsum dolor sit amet.</div>
      </details>
      <button type="submit">Go</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'App',
  computed: {
    imageUrl() {
      const baseUrl = 'https://picsum.photos'
      const grayscale = this.grayscale ? '?grayscale' : ''
      return `${baseUrl}/${this.width}/${this.height}${grayscale}`
    }
  },
  data() {
    return {
      width: 320,
      height: 240,
      grayscale: false
    }
  },
  methods: {
    formSubmit() {
      /**
       * This is the main behavior when being used as an actual
       * Chrome extension...
       */
      // eslint-disable-next-line no-undef
      if (typeof chrome.tabs !== 'undefined') {
        // eslint-disable-next-line no-undef
        chrome.tabs.create({ url: this.imageUrl, active: true })
      } else {
        /**
         * This is a fallback behavior for when this is being
         * previewed with `npm run serve`
         */
        window.open(this.imageUrl)
      }
    }
  }
}
</script>

<style lang="scss">
$light: #fff;
$dark: #333;

html,
body {
  background-color: $light;
  color: $dark;
  padding: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
#app {
  width: 200px;
}
h1 {
  font-size: 1.5rem;
}
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
