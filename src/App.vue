<template>
  <div id="app" style="font-family: sans-serif">
    <app-header />
    <router-view />
  </div>
</template>

<script>
// icons
import '@/assets/font-icons/style.css';
//Components
import header from '@/components/header.vue'

export default {
  data() {
    return { }
  },
  components: {
    appHeader: header
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

#app {
  background-color: #F7F7F7;
}

</style>

