
<template>
  <div class="cart">
    <h2>This Is Cart</h2>
  <button @click="clg(cart[0] === cart[2])">clg</button>
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
    }

}
</script>
