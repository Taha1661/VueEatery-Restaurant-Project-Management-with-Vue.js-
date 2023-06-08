<template>
    <Header />
    <h2>Login Page</h2>
    <div class="login">
        <input type="text" placeholder="Enter Email" v-model="email">
        <input type="password" placeholder="Enter Password" v-model="password">
        <button v-on:click="login()">Log in</button>
        <p>
            <router-link to="/sign-up">Sign up</router-link>
        </p>
    </div>
</template>

<script>
/* eslint-disable */

import Header from './Header.vue';
import axios from 'axios';
export default {
    name: 'Login',
    components: {
        Header
    },
    data() {
        return {
            email: '',
            password: ''
        }
    },
    methods: {
        async login() {
            let result = await axios.get(`http://localhost:3000/users?email=${this.email}&password=${this.password}`)
            if (result.status == 200 && result.data.length > 0) {
                localStorage.setItem('user-info', JSON.stringify(result.data[0]))
                this.$router.push({ name: 'Home' })
            }
            console.warn(result)
        }

    }
}
</script>