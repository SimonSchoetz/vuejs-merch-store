
<template>
<div class="product">
    <h2>{{productName}}s</h2>
    <form class="product-card"> 
        <img width="400" :src="productTypes[selectedType].img" />
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
                @focus="updateProduct(color, i)"
                @blur="showColorPalette(false)"
                :class="{hideColors: color !== currColor}" 
                @mouseover="updateProduct(color, i)" v-for="(type, i) in productTypes" 
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
            <p>Quantity: {{productTypes[selectedType].quantity}}
            </p>
        </div>
    </form>
    <!-- {{testComputed}} -->
    <button @click="clg(colors)">clg</button>
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
            selectedType: 0,
            currColor: "initial",
        }
    },
    methods: {
        clg(input) {
            return console.log(input)
        },
        updateProduct(color, id) {
            return (
                this.selectedType = id,
                this.currColor = color
            )
        },
        showColorPalette(input) {
            input ? this.currColor = input : this.currColor = "initial"
        }
    },
    computed: {
        colors() {
            let colors = [];
            this.merchStock.types.map(type => {
                colors.includes(type.colorMain) ? null : colors.push(type.colorMain)
            });
            console.log("color runs")
            return colors
        },
    }
}
</script>

