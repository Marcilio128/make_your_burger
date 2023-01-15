<template>
    <div id="nav">
    <router-link to="/" id="logo-url">
        <img id="logo" :alt="alt" :src="logo" />
    </router-link>
    <router-link to="/">Home</router-link> | 
    <router-link to="/Pedidos">Pedidos</router-link>
  </div>
</template>

<script>
import NavBarCSS from '../css/NavBar.css';

    export default {
        Name: "NavBar",
        props: ["logo", "alt"],
        components: {
            NavBarCSS
        }
    }
</script>