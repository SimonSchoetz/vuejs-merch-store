
<template>
  <div class="cart">
      <h2>This is Cart ({{cartAmount}})</h2>
  <button @click="clg('scurr')">clg</button>
  </div>
</template>

<script>
export default {
    name: "Cart",
    props: [
      "cartItems",
    ],
    data() { return {
      cart: this.cartItems,
    }},
    methods: {
        clg(input) {
            return console.log(input)
        },
    },
    computed: {
      cartAmount() {
        return this.cartItems.length
      }
    }

}
</script>
