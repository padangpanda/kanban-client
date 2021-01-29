<template>
  <div>
    <Navbar @checkAuth="emitCheckAuth" @fetchCategory="emitFetchCategory" :baseUrl="baseUrl"></Navbar>
    <div class="container-fluid" style="background-color: purple;">
      
    </div>
  </div>

</template>

<script>
import TaskCard from "../components/TaskCard"
import Navbar from "../components/Navbar"

export default {
  name: "Home",
  props: ["category", "baseUrl"],
  components: { 
    Navbar,
    TaskCard
  },
  data() {
    return {
      backlog: [],
      todo: [],
      doing: [],
      done: []
    }
  },
  methods: {
    emitCheckAuth() {
      this.$emit('checkAuth')
    },
    emitFetchCategory() {
      this.$emit('fetchCategory')
    }
  }
}
</script>

<style>

</style>