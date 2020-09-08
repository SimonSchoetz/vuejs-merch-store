
<template>
<div class="product">
    <h2>{{productName}}s</h2>
    <div class="product-card"> 
        <img width="400" :src="productTypes[selectedType].img" />
        <div> 
            <div class="color-container" @mouseenter="showColorPalette(color)" @mouseleave="showColorPalette(false)" v-for="(color, i) in colors()" :key="i">
                
                <div class="color-cover" :class="{hideColors: color === currColor}" :style="{backgroundColor:color}" > </div>
                <div class="main-color" :class="{hideColors: color !== currColor}" @mouseover="updateProduct(i)" v-for="(type, i) in productTypes" v-show="type.colorMain === color" :style="{backgroundColor:type.colorMain}" :key="i"> 
                    <div class="color-logo-1" :class="{hideColors: color !== currColor}" :style="{backgroundColor:type.colorLogo1}"> 
                        <div class="color-logo-2" :class="{hideColors: color !== currColor}" v-show="type.colorLogo2" :style="{backgroundColor:type.colorLogo2}"></div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <button @click="clg(currColor)">clg</button>
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
            colors: () => {
                    let colors = [];
                    this.merchStock.types.map(type => {
                        colors.includes(type.colorMain) ? null : colors.push(type.colorMain)
                    });
                    return colors
            },
            
        }
    },
    methods: {
        clg(input) {
            return console.log(input)
        },
        updateProduct(id) {
            return this.selectedType = id
        },
        showColorPalette(input) {
            input ? this.currColor = input : this.currColor = "initial"
        }
    },
    // computed: {

    // }
}
</script>

