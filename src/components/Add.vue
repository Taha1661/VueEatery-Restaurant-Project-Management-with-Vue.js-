<template>
    <Header />
    <h2>Welcome to Add page</h2>
    <form class="add">
        <input type="text" name="name" placeholder="Enter name" v-model="restaurant.name" />
        <input type="text" name="address" placeholder="Enter Address" v-model="restaurant.address" />
        <input type="text" name="contact" placeholder="Enter Contact" v-model="restaurant.contact" />
        <button type="button" v-on:click="addrestaurant()">Add new restaurant</button>
    </form>
</template>

<script>
/* eslint-disable */

import Header from './Header.vue';
import axios from 'axios'
export default {
    name: 'Add',
    components: {
        Header
    },
    data() {
        return {
            restaurant: {
                name: '',
                address: '',
                contact: ''
            }
        }
    },
    methods: {
        async addrestaurant() {
            console.warn("restaurant details", this.restaurant)
            const result = await axios.post("http://localhost:3000/restaurant", {
                name: this.restaurant.name,
                address: this.restaurant.address,
                contact: this.restaurant.contact
            })
            if (result.status == 201) {
                this.$router.push({ name: 'Home' })
            }
            console.warn("result", result)
        }
    }
}
</script>

<style></style>