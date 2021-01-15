<template>
  <div class="modal fade" id="editModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true" >
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">Edit Task</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <form>
                    <div class="mb-3">
                        <label for="recipient-name" class="col-form-label">Title:</label>
                        <input type="text" class="form-control" v-model="editTitle" :placeholder="dataTask.title">
                    </div>
                    <div class="mb-3">
                        <label for="message-text" class="col-form-label">Description:</label>
                        <textarea class="form-control" v-model="editDescription" :placeholder="dataTask.description"></textarea>
                    </div>
                    </form>
                </div>
                <div class="d-flex  flex-row justify-content-between md-3" style="background-color: grey; height: 50px">
                    <div class="dropdown">
                        <button type="button" 
                            class="btn btn-warning drpdown-toggle" 
                            data-bs-toggle="dropdown"
                            aria-expanded="false"
                            style="height: 50px;"
                        >Move</button>
                        <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton">
                            <li v-for="item in category" :key="item.id" v-show="item.id != dataTask.CategoryId"><a href="#" class="dropdown-item" @click.prevent="patchTask(item.id)" data-bs-dismiss="modal">{{item.name}}</a></li>
                        </ul>
                    </div>
                    <button type="button" class="btn btn-danger"  @click="deleteTask" data-bs-dismiss="modal">Delete</button>
                    <button type="button" class="btn btn-primary" @click.prevent="newTask" data-bs-dismiss="modal">Save</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    props: ['dataTask', 'category', 'baseUrl'],
    name: 'ModalDetailTask',
    data() {
        return {
            editTitle: this.title,
            editDescription: this.description
        }
    },
    methods: {
        deleteTask() {
            axios({
                method: 'DELETE',
                url: `${this.baseUrl}/tasks/${this.dataTask.id}`,
                headers: {
                    access_token: localStorage.access_token
                }
            })
            .then(({data}) => {
                this.$emit('fetchCategory')
            })
            .catch(err => console.log(err))
        },
        patchTask(moveTo) {
            axios({
                method: 'PATCH',
                url: `${this.baseUrl}/tasks/${this.dataTask.id}`,
                headers: {
                    access_token: localStorage.access_token
                },
                data: {
                    CategoryId: moveTo
                }
            })
            .then(({data}) => {
                console.log(data, "<<<<< moved task");
                this.$emit('fetchCategory')
            })
            .catch(err => console.log(err))
        }
    }
}
</script>

<style>

</style>