
<template>
  <div class="cart">
    <h2>This Is Cart</h2>
  <button @click="clg(cart)">clg</button>
  <ul >
    <li class="cart-item" v-for="(item, i) in cart.items" :key="i">
      <img 
      :src="item.item.img" 
      :alt="
        item.item.colorLogo2 === '' ?
        item.item.colorMain.charAt(0).toUpperCase()+
        item.item.colorMain.slice(1)+
        ' '+
        item.item.product.charAt(0).toLowerCase()+
        item.item.product.slice(1)+
        ' whith a '+
        item.item.colorLogo1+ 
        ' Busted Fingerz Logo' : 
        item.item.colorMain.charAt(0).toUpperCase()+
        item.item.colorMain.slice(1)+
        ' '+
        item.item.product.charAt(0).toLowerCase()+
        item.item.product.slice(1)+
        ' whith a '+
        item.item.colorLogo1+ 
        ' and '+
        item.item.colorLogo2+
        ' Busted Fingerz Logo'" 
        />
      <!-- <div> {{item.item.colorMain}}, {{item.item.colorLogo1}}, {{item.item.colorLogo2}} </div> -->
      <div> {{item.amount}} </div>
    </li>
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
