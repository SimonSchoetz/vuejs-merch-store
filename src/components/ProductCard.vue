
<template>
<div class="product">
    <h2>{{productName}}s</h2>
    <div> 
        <img width="200" :src="productTypes[selectedType].img" />
        <div class="color-container" v-for="(color, i) in colors()" :style="{backgroundColor:color}" :key="i">
            <div @mouseover="updateProduct(type.id)" class="main-color" v-for="(type, i) in productTypes" v-show="type.colorMain === color" :style="{backgroundColor:type.colorMain}" :key="i"> 
                <div class="color-logo-1" :style="{backgroundColor:type.colorLogo1}"> 
                    <div class="color-logo-2" v-show="type.colorLogo2" :style="{backgroundColor:type.colorLogo2}"></div>
                </div>
            </div>

        </div>
        
    </div>
    
    <button @click="clg(colors())">clg</button>
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
        }
    },
    // computed: {

    // }
}
</script>

