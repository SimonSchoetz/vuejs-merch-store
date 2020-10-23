
<template>
  <div class="cart">
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
            <button 
              class="amount-controls" 
              @click="changeAmount(item, 'less')"
              :disabled="!item.amount">-</button> 
            {{item.amount}}
            <button 
              class="amount-controls" 
              @click="changeAmount(item, 'more')"
              :disabled="!item.item.quantity">+
            </button> 
          </span>
        </div>
        <div class="delete-container" v-show="!item.amount">
          <button>Delete from Cart</button>
        </div>
      </div>
    </li>
  </ul>
  <div class="sub-total">
    <h2><span>Subtotal:</span> <span>{{subtotal}} € </span></h2>
    <button class="checkout" @click="showCheckout(true)">Checkout</button> 
  </div>
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
          return console.log(input);
        },
        changeAmount(item, action) {
          if (action === "less") {
            item.amount > 0 ? item.amount -- : null;
            item.item.quantity ++;
          }
          if (action ==="more") {
            if (item.item.quantity <= 0) return
            else {
            item.amount ++;
            item.item.quantity --;
            }
          }
        },
        showCheckout(input) {
          console.log(input)
        }
    },
    computed: {
      subtotal() {
        let total = 0;
        this.cart.items.forEach(item => {
          total += item.item.prize*item.amount
        })
        return total.toFixed(2)
      }
    }

}
</script>
