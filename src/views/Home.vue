<template>
    <Banner />
<div class="main-container">
    <h1>Monte o seu Hamburger:</h1>
    <Form />
 </div>
</template>

<script>
import Banner from '../components/Banner.vue';
import Form from '../components/Form.vue';

 export default {
    Name: 'Home',
    banner_src: './public/img/Hamburger.jpg',
    components: {
        Banner,
        Form,
    }
 }
</script>
