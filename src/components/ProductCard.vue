
<template>
<div class="product">
    <h2>{{productName}}s</h2>
    <div class="product-card"> 
        <div class="product-view"> 
            <img width="400" v-show="hovering" :src="currItem.img" />
            <img width="400" v-show="!hovering" :src="lockedItem.img" />
            <div class="out-of-stock-layer" v-if="!inStock"> 
                <p> 
                    Out of stock! 
                </p>
            </div>
            <div class="color-picker">  
            <div 
                class="color-container" 
                @mouseenter="handleColorHover(color, true)" 
                @mouseleave="handleColorHover('initial', false)" 
                v-for="(color, i) in colors" 
                :key="i"
            >
                <button class="color-cover" 
                @click="handleColorHover(color, true)" :class="{hideColors: color === currColor}" :style="{backgroundColor:color}" > 
                </button>

                <button 
                class="main-color"
                :class="{hideColors: color !== currColor}" 
                @focus="updateProduct(color, i)"
                @blur="handleColorHover('initial', false)"
                @mouseover="updateProduct(color, i)"
                v-for="(type, i) in productTypes" 
                @click="lockItem(currItem, i, 'lock')"
                v-show="type.colorMain === color" 
                
                :style="{backgroundColor:type.colorMain}" 
                :key="i"> 
                    <div class="color-logo-1" :class="{hideColors: color !== currColor}" :style="{backgroundColor:type.colorLogo1}"> 
                        <div class="color-logo-2" :class="{hideColors: color !== currColor}" v-show="type.colorLogo2" :style="{backgroundColor:type.colorLogo2}" />
                    </div>
                </button>
            </div>
            
        </div>
        </div>
    </div>
    <!-- {{testComputed}} -->
    <button @click="clg(this.lockedItem)">clg</button>
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
            hovering: false,
            lockedItem: this.merchStock.types[0],
            inStock: true,
        }
    },
    methods: {
        clg(input) {
            return console.log(input)
        },
        updateProduct(color, id) {
            this.handleColorHover('color', true);
            return (
                this.selectedId = id,
                this.currColor = color
            )
        },
        showColorPalette(input) {
            input ? this.currColor = input : this.currColor = "initial"
        },
        lockItem(item, i, lock) {
            if (lock === "lock" && this.inStock) {
                console.log(this.lockedItem)
                this.lockedItem = item;
                this.currItem = item;
                this.handleColorHover('initial', false);
            }
        },
        handleColorHover(color, isOn) {
            if (isOn) {
                this.hovering = true;
                this.showColorPalette(color);
                this.outOfStock(this.currItem.quantity)
            }
            if (!isOn) {
                this.hovering = false
                this.showColorPalette(color)
                this.inStock = true
            }

        },
        addToCart() {
            this.$emit("add-to-cart", this.currItem) //works but has to go to a global shopping cart
            // needs to count down the amount of stock
            // needs to count up if some articles are chosen multiple times
        },
        outOfStock(quantity) {
            if (quantity <= 0) return this.inStock = false
            else return this.inStock = true
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
        },
    }
}
</script>

