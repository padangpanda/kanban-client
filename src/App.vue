<template>
    <div>
        <login v-if="currentPage === 'login'" :baseUrl="baseUrl" @checkAuth="checkAuth"></login>
        <home v-else :tasks="tasks" :category="category" :baseUrl="baseUrl" @checkAuth="checkAuth" @fetchCategory="fetchCategory"></home>
    </div>
</template>

<script>
import axios from 'axios'
import Login from './views/Login.vue'
import Home from './views/Home.vue'

export default {
    name: "App",
    data() {
        return {
            baseUrl: "https://immense-journey-98337.herokuapp.com",
            // baseUrl: "http://localhost:3000",
            currentPage: "login",
            tasks: [],
            category: []
        }
    },
    components: {
        Login,
        Home
    },
    created() {
        this.checkAuth()
        this.fetchCategory()
    },
    methods: {
        checkAuth() {
            if (localStorage.access_token) {
                this.changePage('home')
            } else {
                this.changePage('login')
            }
        },
        fetchTasks() {
            axios({
                method: "GET",
                url: `${this.baseUrl}/tasks`,
                headers: {
                    access_token: localStorage.access_token
                }
            })
            .then(({ data }) => {
                this.tasks = data
            })
            .catch(err => console.log(err))
        },
        fetchCategory() {
            axios({
                method: "GET",
                url: `${this.baseUrl}/category`
            })
            .then(({ data }) => {
                console.log(data);
                this.category = data
            })
            .catch(err => console.log(err))
        },
        changePage(page) {
            this.currentPage = page
        }
    }
}
</script>

<style>

</style>