<script setup>
import { RouterLink } from 'vue-router';
</script>
<template>
    <div class="center-container">
        <h1>Welcome to Vue Post CRUD tutorial.</h1>
        <RouterLink :to="'/posts'" class="btn btn-green">Go To Posts</RouterLink>
    </div>
</template>