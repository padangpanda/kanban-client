<template>
    <nav class="navbar navbar-expand-lg navbar-light" style="background-color: grey;">
      <div class="container">
        <a class="navbar-brand" href="#" style="margin-left: 15px;">Kanban</a>
      </div>
      <div id="modal">
        <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal" style="width: 120px; margin-right: 10px;">New Task</button>
        <modal-new-task :baseUrl="baseUrl" @fetchCategory="emitFetchCategory"></modal-new-task>

      </div>
      <button type="button" class="btn btn-danger" style="margin-right: 30px;" @click="logout">Logout</button>
    </nav>
</template>

<script>
import axios from "axios"
import ModalNewTask from './ModalNewTask.vue';

export default {
  components: { ModalNewTask },
  props: ['baseUrl'],
  name: "Navbar",
  methods: {
    logout() {
      console.log('logout');
      localStorage.clear()
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