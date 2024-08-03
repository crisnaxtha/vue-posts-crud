<script setup>
import axios from 'axios';
import { onMounted, reactive } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();

const postId = route.params.id;
const state = reactive({
    post: Object
})

onMounted(async () => {
    try {
        const response = await axios.get(`http://localhost:8080/posts/${postId}`);
        state.post = response.data;
    } catch (error) {
        console.log("Error while fetching: ", error);
    }
})


</script>
<template>
    <div class="center-container">
        <h1>{{ state.post.title }}</h1>
        <p>{{ state.post.description }}</p>
        <RouterLink :to="`/posts`" class="btn btn-green">Return to Posts</RouterLink>
    </div>
</template>