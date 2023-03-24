<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
    <nav class="page-navbar" data-spy="affix" data-offset-top="10">
        <ul class="nav-navbar container">
            <li class="nav-item"><a href="/" class="nav-link">Home</a></li>
            <li class="nav-item"><a href="recipes" class="nav-link">Recipe</a></li>
            <li class="nav-item"><a href="/" class="nav-link"><img src="./assets/imgs/logo.png" ></a></li>
            <li class="nav-item"><a href="profile" class="nav-link">Profile</a></li>
            <li class="nav-item"><a href="signin" class="nav-link">Login/Logout</a></li>
            
        </ul>
    </nav>

  <RouterView />
</template>
<style>
@import './assets/vendors/themify-icons/css/themify-icons.css';
@import './assets/css/dorang.css';
</style>
