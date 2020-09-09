
<template>
<div class="product">
    <h2>{{productName}}s</h2>
    <div class="product-card"> 
        <img width="400" :src="currItem.img" />
        <div class="color-picker">  
            <div 
            class="color-container" 
            @mouseenter="showColorPalette(color)" 
            @mouseleave="showColorPalette(false)" v-for="(color, i) in colors" 
            :key="i">
                <div class="color-cover" :class="{hideColors: color === currColor}" :style="{backgroundColor:color}" > 
                </div>
                <button 
                class="main-color"
                :class="{hideColors: color !== currColor}" 
                @focus="updateProduct(color, i)"
                @blur="showColorPalette(false)"
                @mouseover="updateProduct(color, i)" v-for="(type, i) in productTypes" 
                @click="addToCart(currItem.id)"
                v-show="type.colorMain === color" 
                :style="{backgroundColor:type.colorMain}" 
                :key="i"> 
                    <div class="color-logo-1" :class="{hideColors: color !== currColor}" :style="{backgroundColor:type.colorLogo1}"> 
                        <div class="color-logo-2" :class="{hideColors: color !== currColor}" v-show="type.colorLogo2" :style="{backgroundColor:type.colorLogo2}" />
                    </div>
                </button>
            </div>
        </div>
        <div class="product-details"> 
            <p v-show="currItem.quantity <= 0"> Out of stock! </p>
            <p v-show="currItem.quantity > 0"> Click on color to add to card </p>
        </div>
    </div>
    <!-- {{testComputed}} -->
    <button @click="clg(shoppingCart)">clg</button>
</div>  
</template>

<script>
export default {
    name: "ProductCard",
    props: [
        "merchStock",
    ],
    data() {
        return {
            products: this.merchStock,
            productName: this.merchStock.product,
            productTypes: this.merchStock.types,
            selectedId: 0,
            currColor: "initial",
            shoppingCart: [],
        }
    },
    methods: {
        clg(input) {
            return console.log(input)
        },
        updateProduct(color, id) {
            return (
                this.selectedId = id,
                this.currColor = color
            )
        },
        showColorPalette(input) {
            input ? this.currColor = input : this.currColor = "initial"
        },
        addToCart() {
            this.$emit("add-to-cart", this.currItem) //works but has to go to a global shopping cart
            // needs to count down the amount of stock
            // needs to count up if some articles are chosen multiple times
        }
    },
    computed: {
        colors() {
            let colors = [];
            this.merchStock.types.map(type => {
                colors.includes(type.colorMain) ? null : colors.push(type.colorMain)
            });
            return colors
        },
        currItem() {
            return this.productTypes[this.selectedId]
        }
    }
}
</script>

