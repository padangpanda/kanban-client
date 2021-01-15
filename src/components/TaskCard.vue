<template>
    <div class="card mb-1">
        <div class="card-body">
            <h5 class="card-title">{{dataTask.title}}</h5>
            <h6 class="card-subtitle mb-2 text-muted">Description</h6>
            <p class="card-text">{{dataTask.description}}</p>
            <div id="modal">
                <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#editModal" style="width: 120px; margin-right: 10px;">Show Details</button>
                <modal-detail-task :category="category" :dataTask="dataTask" :baseUrl="baseUrl" @fetchCategory="emitFetchCategory"></modal-detail-task>
            </div>
        </div>  
    </div>  
</template>

<script>
import ModalDetailTask from './ModalDetailTask.vue'

export default {
    components: { ModalDetailTask },
    props: ['dataTask', 'category', 'baseUrl'],
    name: "TaskCard",
    methods: {
        emitFetchCategory() {
            this.$emit('fetchCategory')
        }
    }
}
</script>

<style>

</style>