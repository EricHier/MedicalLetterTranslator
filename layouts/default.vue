<template>
  <div class="font-body">
    <Header></Header>
    <nuxt/>
    <Footer/>
  </div>
</template>
<script>
  import Footer from "../components/gui-elements/Footer"
  import Header from "../components/gui-elements/Header"

  require("animate.css/animate.min.css")

  require("typeface-lato");

  export default {
    components: {
      Footer,
      Header
    }
  }
</script>
<style>
  html {
    background-color: #fafafa;
  }
</style>
