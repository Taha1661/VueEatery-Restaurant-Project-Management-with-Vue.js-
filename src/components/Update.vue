<template>
    <Header />
    <h2>Welcome to Update page</h2>
    <form class="update">
        <input type="text" name="name" placeholder="Enter name" v-model="restaurant.name" />
        <input type="text" name="address" placeholder="Enter Address" v-model="restaurant.address" />
        <input type="text" name="contact" placeholder="Enter Contact" v-model="restaurant.contact" />
        <button type="button" v-on:click="updaterestaurant()">Add new restaurant</button>
    </form>
</template>

<script>
/* eslint-disable */

import Header from './Header.vue';
import axios from 'axios'
export default {
    name: 'Update',
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
        async updaterestaurant() {
            const result = await axios.put("http://localhost:3000/restaurant/" + this.$route.params.id, {
                name: this.restaurant.name,
                address: this.restaurant.address,
                contact: this.restaurant.contact
            })
            if (result.status == 200) {
                this.$router.push({ name: 'Home' })
            }
            console.warn("result", result)
        }
    },
    async mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({ name: 'Signup' })
        }
        const result = await axios.get('http://localhost:3000/restaurant/' + this.$route.params.id)
        // console.warn(this.$route.params.id)
        console.warn(result.data)
        this.restaurant = result.data
    }
}
</script>

<style></style>