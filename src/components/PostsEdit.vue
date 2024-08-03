<script setup>
import axios from 'axios';
import { onMounted, reactive } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();

const postId = route.params.id;

const form = reactive({
    title: '',
    description: ''
})

onMounted( async () => {
    try {
        const response = await axios.get(`http://localhost:8080/posts/${postId}`);
        form.title = response.data.title;
        form.description = response.data.description;
    } catch (error) {
        console.log("Error fetching post", response);
    }
})

const handleSubmit = async () => {
    const updatePost = {
        title: form.title,
        description: form.description
    }

    try {
        const response = await axios.put(`http://localhost:8080/posts/${postId}`, updatePost);
        router.push(`/posts/${response.data.id}`);
    } catch (error) {
        console.error("Error updating post", error);
    }
}

</script>
<template>
    <RouterLink :to="`/posts`" class="btn btn-green">Return to Posts</RouterLink>
    <div>
        <form @submit.prevent="handleSubmit">
            <label for="title">Title</label>
            <input 
            v-model="form.title" 
            type="text" 
            id="title" 
            name="title" 
            placeholder="Title">
            <label for="description">Description</label>
            <textarea 
            v-model="form.description" 
            id="description" 
            name="description">
            </textarea>
            <button type="submit" class="btn btn-green">Submit</button>
        </form>
    </div>
</template>