
<template>
  <div id="app">
    <Head />
    <Products />
  </div>
</template>

<script>

import Head from './components/Head.vue';
import Products from './components/Products';

export default {
  name: 'App',
  components: {
    Head,
    Products
  }
}
</script>

<style lang="scss">
  @import "./style.scss"
</style>
