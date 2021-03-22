<template>
  <div id="app">
    <h1>Lorem Picsum</h1>
    <form action="#" @submit.prevent="formSubmit">
      <div class="form-element">
        <label for="width">Width</label>
        <input
          type="number"
          id="width"
          name="width"
          v-model="width"
          min="1"
          required
          @focus="$event.target.select()"
        />
      </div>
      <div class="form-element">
        <label for="height">Height</label>
        <input
          type="number"
          id="height"
          name="height"
          v-model="height"
          min="1"
          required
          @focus="$event.target.select()"
        />
      </div>
      <div class="form-element">
        <label for="grayscale">
          <input
            type="checkbox"
            id="grayscale"
            name="grayscale"
            v-model="grayscale"
          />
          Grayscale
        </label>
      </div>
      <div class="form-actions">
        <button type="submit" aria-label="Get image">Get image</button>
      </div>
      <details>
        <summary>Advanced options</summary>
        <div>
          <div class="form-element form-element-block">
            <label for="blur"
              >Blur <small>({{ blur }})</small></label
            >
            <input
              type="range"
              name="blur"
              id="blur"
              min="0"
              max="10"
              v-model="blur"
            />
          </div>
          <div class="form-element">
            <label for="seed">Seed</label>
            <input
              type="text"
              name="seed"
              id="seed"
              v-model="seed"
              @focus="$event.target.select()"
            />
          </div>
        </div>
      </details>
    </form>
  </div>
</template>

<script>
export default {
  name: 'App',
  computed: {
    imageUrl() {
      const baseUrl = 'https://picsum.photos'

      let seed = ''
      if (this.seed !== '') {
        seed = `/seed/${this.seed}`
      }

      let queryString = ''
      const queryParams = []
      if (this.grayscale) {
        queryParams.push('grayscale')
      }
      if (this.blur > 0) {
        queryParams.push(`blur=${this.blur}`)
      }
      if (queryParams.length > 0) {
        queryString = '?' + queryParams.join('&')
      }
      return `${baseUrl}${seed}/${this.width}/${this.height}${queryString}`
    }
  },
  data() {
    return {
      width: 320,
      height: 240,
      grayscale: false,
      blur: 0,
      seed: ''
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
$accent: #33c;

html,
body {
  background-color: $light;
  color: $dark;
  padding: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
* {
  margin-top: 0;
}
input[type='text'],
input[type='number'] {
  width: 5rem;
  padding: 0 0 0 0.5rem;
  line-height: 1.5rem;
}
input[type='range'] {
  margin: 0;
  width: 100%;
}
button {
  background-color: $accent;
  border: 2px solid $accent;
  border-radius: 0.25rem;
  color: $light;
  cursor: pointer;
  font-weight: bold;
  padding: 0 0.5rem;
  line-height: 1.5rem;
  transition: all 0.25s ease-in;
  &:hover,
  &:focus {
    background-color: $light;
    color: $accent;
  }
}
h1 {
  font-size: 1.5rem;
}
details {
  border: 1px solid $dark;
  font-size: 0.85rem;
  margin: 1rem 0;
  summary {
    background-color: rgba($accent, 0.2);
    cursor: pointer;
    font-weight: bold;
    padding: 1rem;
    &:focus {
      outline: 3px solid $accent;
    }
  }
  & > div {
    border-top: 1px solid $dark;
    padding: 1rem;
  }
}
#app {
  width: 200px;
}
div.form-element {
  align-items: center;
  display: flex;
  margin-bottom: 1rem;
  & > * {
    box-sizing: border-box;
    flex: 1;
  }
  &.form-element-block {
    display: block;
    label {
      display: block;
      margin-bottom: 0.5rem;
    }
  }
}
</style>
