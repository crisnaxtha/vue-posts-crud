<script setup>
import { onMounted, reactive } from 'vue';
import { RouterLink } from 'vue-router';
import axios from 'axios';
import Post from '@/components/Post.vue';

const state = reactive({
    posts: []
})

onMounted(async () => {
  try {
    const response = await axios.get('http://localhost:8080/posts');
    state.posts = response.data;
  } catch (error) {
    console.error('Error fetching jobs:', error);
  }
});
</script>
<template>
  <div class="center-container">
    <h1>All Post</h1> 
    <RouterLink :to="'/posts/add'" class="btn btn-green">Add Post</RouterLink>
    <br />
    <br />
    <table id="posts">
        <tr>
            <th>S.N</th>
            <th>Title</th>
            <th>Action</th>
        </tr>
        <Post v-for="post in state.posts" :key="post.id" :post="post"/>
    </table>
  </div>
</template>
