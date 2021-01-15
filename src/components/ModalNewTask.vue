<template>
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true" >
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">Add New Task</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <form>
                    <div class="mb-3">
                        <label for="recipient-name" class="col-form-label">Title:</label>
                        <input type="text" class="form-control" v-model="title">
                    </div>
                    <div class="mb-3">
                        <label for="message-text" class="col-form-label">Description:</label>
                        <textarea class="form-control" v-model="description"></textarea>
                    </div>
                    </form>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                    <button type="button" class="btn btn-primary" @click.prevent="newTask" data-bs-dismiss="modal">Submit</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: "ModalNewTask",
    props: ['baseUrl'],
    data() {
        return {
            title: '',
            description: ''
        }
    },
    methods: {
        newTask() {
            axios({
                method: 'POST',
                url: `${this.baseUrl}/tasks`,
                data: {
                    title: this.title,
                    description: this.description
                },
                headers: {
                    access_token: localStorage.access_token
                }
            })
            .then(({data}) => {
                console.log('new task masuk');
                this.$emit('fetchCategory')
            })
            .catch(err => console.log(err))
        }
    }
}
</script>

<style>

</style>