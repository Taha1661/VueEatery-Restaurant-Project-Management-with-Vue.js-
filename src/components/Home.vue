<template>
    <Header />
    <h2>Hello {{ name }} , Welcome to home page</h2>
    <table border="1">
        <thead>
            <tr>
                <th>Id</th>
                <th>Name</th>
                <th>Contact</th>
                <th>Address</th>
                <th>Action</th>
            </tr>
        </thead>
        <tr v-for="item in restaurant" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.contact }}</td>
            <td>{{ item.address }}</td>
            <td>
                <button class="action"><router-link :to="'/update/' + item.id">Update</router-link></button>
                <button v-on:click="deletrestaurant(item.id)" class="action">Delete</button>

            </td>
        </tr>
    </table>
</template>

<script>
/* eslint-disable */

import { thisExpression } from '@babel/types';
import Header from './Header.vue';
import axios from 'axios'
export default {
    name: 'Home',
    data() {
        return {
            name: '',
            restaurant: []
        }
    },
    components: {
        Header
    },
    methods: {
        async deletrestaurant(id) {
            let result = await axios.delete("http://localhost:3000/restaurant/" + id)
            console.warn(result)
            if (result.status == 200) {
                this.loadData()
            }
        },
        async loadData() {
            let user = localStorage.getItem('user-info');
            this.name = JSON.parse(user).name;
            if (!user) {
                this.$router.push({ name: 'Signup' })
            }
            let result = await axios.get("http://localhost:3000/restaurant")
            console.warn(result)
            this.restaurant = result.data;
        }
    },
    async mounted() {
        this.loadData();
    }
}
</script>

<style>
table {
    border-collapse: collapse;
}

th,
td {
    text-align: center;
    border-bottom: 1px solid #ddd;
    width: 160px;
    height: 40px;
}

th {
    background-color: #f2f2f2;
}

tr:hover {
    background-color: #f5f5f5;
}

.action {
    margin: auto;
}
</style>