<template>
  <NavBar :logo="logo_src" :alt="app_name" />
  <router-view />
  <Footer />
</template>

<script>
  import NavBar from "../src/components/NavBar.vue";
  import Footer from "../src/components/Footer.vue";
  import ResetCss from "./css/Reset.css";
 export default {
    Name: "App",
    components: {
      NavBar,
      Footer,
      ResetCss
    },
    data(){
      return {
        logo_src: "/img/logo.png",
        app_name: 'Make Your Burger'
      }
    }
 }
</script>
