<template>
    <Header />
    <img src="../assets/5_restaurant_logo_ZET98E.jpeg" class="logo">
    <h2>Signup </h2>

    <div class="register">
        <input type="text" placeholder="Enter Name" v-model="name">
        <input type="text" placeholder="Enter Email" v-model="email">
        <input type="password" placeholder="Enter Password" v-model="password">
        <button v-on:click="signup()">Sign Up</button>
        <p>
            <router-link to="/login">Login</router-link>
        </p>
    </div>
</template>

<script>
/* eslint-disable */

import Header from './Header.vue';
import axios from 'axios'
export default {
    name: 'Signup',
    components: {
        Header
    },
    data() {
        return {
            name: '',
            email: '',
            password: ''
        }
    },
    methods: {
        async signup() {
            let result = await axios.post("http://localhost:3000/users", {
                email: this.email,
                password: this.password,
                name: this.name
            });
            console.warn(result)
            if (result.status == 201) {
                localStorage.setItem("user-info", JSON.stringify(result.data))
                this.$router.push({ name: 'Home' })
            }
        }
    }
}
</script>

<style></style>