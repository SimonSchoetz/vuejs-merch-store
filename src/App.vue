
<template>
  <div id="app">
    <Head />
    <Shop />
  </div>
</template>

<script>

import Head from './components/Head.vue';
import Shop from './components/Shop';

export default {
  name: 'App',
  components: {
    Head,
    Shop
  }
}
</script>

<style lang="scss">
  @import "./style.scss"
</style>
