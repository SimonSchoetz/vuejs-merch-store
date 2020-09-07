
<template>
<div class="product">
    <h2>This is {{merchStock.product}}</h2>
</div>  
</template>

<script>
export default {
    name: "ProductCard",
    props: [
        "merchStock"
    ],
}
</script>

