
<template>
<div class="product">
    <h2>{{productName}}s</h2>
    <img width="200" :src="productTypes[index].img" />
    <button @click="clg(productTypes)">clg</button>
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
        index: 0
        }
    },
    methods: {
        clg(input) {
            return console.log(input)
        }
    }
}
</script>

