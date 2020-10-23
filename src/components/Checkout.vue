<template>
<div>
    <div class="back-container">
        <button class="back-btn" @click="setCheckout()">BACK TO THE SHOP</button>

    </div>

</div>
</template>

<script>
export default {
name: "Checkout",
methods: {
        setCheckout() {
          this.$emit("set-checkout");
        }
    }
}
</script>

<style>

</style>