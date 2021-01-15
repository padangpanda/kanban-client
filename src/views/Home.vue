<template>
  <div>
    <Navbar @checkAuth="emitCheckAuth" @fetchCategory="emitFetchCategory" :baseUrl="baseUrl"></Navbar>
    <div class="container-fluid" style="background-color: purple;">
      <div class="row">
        <div class="col-3 mt-2" v-for="item in category" :key="item.id">
          <div class="container">
              <div :class="item.categoryClass">
                  {{ item.name }}
              </div>
              <div class="row">
                  <div class="overflow-auto" style="height: 83vh;">
                    <task-card v-for="task in item.Tasks" :key="task.id" :dataTask="task" :category="category" :baseUrl="baseUrl" @fetchCategory="emitFetchCategory"></task-card>
                  </div>
              </div>
          </div>  
        </div>
        
      </div>
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