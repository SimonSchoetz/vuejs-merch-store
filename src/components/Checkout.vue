<template>
<div>
    <div class="btn-container">
        <button class="back-btn" @click="setCheckout()">BACK TO THE SHOP</button>
    </div>
    <form @submit="handleSubmit(true)">
        <div :class="showFinal ? 'left-side' : 'left-side active'">
            <label for="first-name">
                <span class="required">*<span>First Name</span> </span> 
                <input required type="text" id="first-name" v-model="firstName" placeholder="First Name" />
            </label>
            <label for="last-name">
                <span class="required">*<span>Last Name</span></span>  
                <input required type="text" id="last-name" v-model="lastName" placeholder="Last Name" />
            </label>
            <label for="email">
                <span class="required">*<span>Email Address</span> </span> 
                <input required type="text" id="email" v-model="email" placeholder="Email Address" />
            </label>
            <label for="street">
                <span class="required">*<span>Street Name and No.</span></span>
                <input required type="text" id="street" v-model="street" placeholder="Street and No." />
            </label>
            <label for="zip-code">
                <span class="required">*<span>Zip Code</span></span>  
                <input required type="text" id="zip-code" v-model="zipCode" placeholder="Zip Code" />
            </label>
            <label for="country">
                <span class="required">*<span>Country</span></span>  
                <input required type="text" id="country" v-model="country" placeholder="Country" />
            </label>
            <div class="btn-container bottom-btn">
                <div class="required-next">
                    <span class="required">* REQUIRED</span>
                    <button type="button" class="next-btn" :disabled="disableNext" @click="setShowFinal(true)">NEXT >></button>
                </div>
            </div>
        </div>
        <div :class="showFinal ? 'right-side active' : 'right-side'">
            <div class="final-tabel">
                <h2>OVERVIEW</h2>
                <h3>POST ADDRESS:</h3>
                <ul class="post-address">
                    <li>{{firstName}} {{lastName}}</li>
                    <li>{{street}}</li>
                    <li>{{zipCode}} {{country}}</li>
                </ul>
                <h3>TO PAY:</h3>
                <ul class="to-pay">
                    <li><span>Subtotal:</span><span>{{this.subTotal}} €</span></li>
                    <li><span>Tax (16%)</span>{{this.tax}} €</li>
                    <li><span>Total:</span><span>{{this.total}} €</span></li>
                </ul>
            </div>
            <div class="btn-container bottom-btn">
                <div class="back-order">
                    <button type="button" class="back-btn" @click="setShowFinal(false)"> &lt;&lt; BACK</button>
                    <input class="submit-btn" type="submit" value="ORDER">
                </div>
            </div>
        </div>
    </form>
    <div v-show="submitted" class="end-card" @click="handleSubmit(false)">
        <h1>Thx for trying my online shop made with Vue.js!</h1>
        <p>No real order has been issued ;)</p>
    </div>
</div>
</template>

<script>
export default {
    name: "Checkout",
    props: [
        "subTotal",
    ],
    data() { return {
        firstName: "",
        lastName: "",
        email: "",
        street: "",
        zipCode: "",
        country: "",
        showFinal: false,
        submitted: false
    }},
    methods: {
        setCheckout() {
            this.$emit("set-checkout");
        },
        handleSubmit(input) {
            this.submitted = input;
            console.log(input)
        },
        setShowFinal(input) {
            this.showFinal = input;
        }
    },
    computed: {
        tax() {
            return (this.subTotal * 0.16).toFixed(2)
        },
        total() {
            return (parseFloat(this.subTotal) + parseFloat(this.tax))
        },
        disableNext() {
            if (this.firstName === "" || this.lastName === "" || this.email === "" || this.street === "" || this.zipCode === "" || this.country === "" || this.showFinal === "") return true 
            else return false
        }
    }
}
</script>

<style>

</style>