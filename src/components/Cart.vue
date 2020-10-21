
<template>
  <div class="cart">
    <h2>This Is Cart</h2>
  <button @click="clg(cart)">clg</button>
  <ul v-for="(item, i) in cart.items" :key="i">
    <li> {{item.item.product}}</li>
    <li> {{item.item.colorMain}}, {{item.item.colorLogo1}}, {{item.item.colorLogo2}} </li>
  </ul>
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
