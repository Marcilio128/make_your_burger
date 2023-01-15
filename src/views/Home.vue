<template>
    <Banner />
<div class="main-container">
    <h1>Monte o seu Hamburger:</h1>
    <p>Formulário</p>
 </div>
</template>

<script>
import Banner from '../components/Banner.vue';

 export default {
    Name: 'Home',
    banner_src: './public/img/Hamburger.jpg',
    components: {
        Banner
    }
 }
</script>
