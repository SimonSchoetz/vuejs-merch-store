
<template>
  <div class="cart">
    <h2>This Is Cart</h2>
  <button @click="clg(cart)">clg</button>
  <ul >
    <li class="cart-item" v-for="(item, i) in cart.items" :key="i">
      <h3> {{item.item.product}}: {{item.item.colorMain}}, {{item.item.colorLogo1}} {{item.item.colorLogo2 !== '' ? 'and '+ item.item.colorLogo2 : null}}</h3>
      <div class="img-container">
        <img 
        width="200"
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
      </div>
      <div class="item-summary">
        <div>
          <span>Single prize:</span>
          <span>{{item.item.prize}} €</span>
        </div>
        <div>
          <span>In cart: </span> 
          <span> 
            <button class="amount-controls">-</button> 
             {{item.amount}}  
            <button class="amount-controls">+</button> 
            </span>
          </div>
      </div>
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
