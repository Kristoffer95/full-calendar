<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
export default {
  data() {
    return { }
  },
  methods: {
    icon(iconName) {
      return require(`./assets/SVG/${iconName}.svg`)
    }
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

</style>

