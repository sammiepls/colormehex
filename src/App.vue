<template>
  <div id="app" :style="containerStyles">
   <h1>Color me HEX</h1>
   <form @submit.prevent>
    <label>
      <span class="hidden">Type a name</span>
      <input placeholder="Type your name" type="text" v-model="name" />
    </label>

    <label v-show="hexName">
      Your hex color is
      <output>{{ hexName }}</output>
    </label>
   </form>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      name: ''
    }
  },
  computed: {
    hexName () {
      let hexName = this.name.toLowerCase()
      if (this.name.length < 6) return false

      return `#${hexName.replace(/([^a-e])/g, 0).substr(0, 6)}`
    },
    containerStyles () {
      if (!this.hexName) return {}

      return {
        background: this.hexName
      }
    }
  }
}
</script>

<style lang="scss">
  $spacing: 1.25rem;
  $font-color: #2c3e50;

  .hidden {
    position: absolute;
    overflow: hidden;
    clip: rect(0 0 0 0);
    height: 1px;
    width: 1px;
    margin: -1px;
    padding: 0;
    border: 0;
  }

  #app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: $font-color;
    min-height: 100vh;
    display: flex;
    flex-flow: column;
    align-items: center;
    justify-content: center;
  }

  h1 {
    margin: $spacing 0;
    text-transform: uppercase;
    letter-spacing: 0.5em;
    font-size: 1em;
  }

  form {
    input {
      padding: $spacing / 2;
    }

    label {
      display: block;
      margin: $spacing / 2 0;
      & > * {
        display: block;
      }
      &:last-child {
        margin: $spacing 0;
      }
    }

    output {
      font-size: 3rem;
      font-weight: bold;
    }
  }
</style>
