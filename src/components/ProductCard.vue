
<template>
<div class="product">
    <h3 class="product-name">{{productName}}s</h3>
    <div class="product-card"> 
        <div class="product-view"> 
            <img width="400" 
                :src="imgSrc.img" 
                :alt="
                    imgSrc.colorLogo2 === '' ?
                    imgSrc.colorMain.charAt(0).toUpperCase()+
                    imgSrc.colorMain.slice(1)+
                    ' '+
                    imgSrc.product.charAt(0).toLowerCase()+
                    imgSrc.product.slice(1)+
                    ' whith a '+
                    imgSrc.colorLogo1+ 
                    ' Busted Fingerz Logo' : 
                    imgSrc.colorMain.charAt(0).toUpperCase()+
                    imgSrc.colorMain.slice(1)+
                    ' '+
                    imgSrc.product.charAt(0).toLowerCase()+
                    imgSrc.product.slice(1)+
                    ' whith a '+
                    imgSrc.colorLogo1+ 
                    ' and '+
                    imgSrc.colorLogo2+
                    ' Busted Fingerz Logo'"  />
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
                    <div class="color-cover" 
                    :class="{hideColors: color === currColor}" 
                    @click="handleColorHover(color, true)" 
                    :style="{backgroundColor:color}" > 
                    </div>
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
            <button class="to-cart-btn" :disabled="!inStock" @click="addToCart()">
                ADD TO CART
            </button>
        </div>
    </div>
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
        updateProduct(color, id) {
            this.handleColorHover('color', true);
            return (
                this.selectedId = id,
                this.currColor = color
            )
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
        showColorPalette(input) {
            input ? this.currColor = input : this.currColor = "initial"
        },
        lockItem(item, i, lock) {
            if (lock === "lock" && this.inStock) {
                this.lockedItem = item;
                this.currItem = item;
                this.handleColorHover('initial', false);
            }
        },
        addToCart() {
            this.$emit("add-to-cart", this.currItem);
            this.currItem.quantity --;
            console.log("Remaining quantity: "+this.currItem.quantity)
            this.outOfStock(this.currItem.quantity);
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
        imgSrc() {
            return this.hovering? this.currItem : this.lockedItem
        }
    }
}
</script>

