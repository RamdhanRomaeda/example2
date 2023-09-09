<template>
    <div id="app">
      <Header />
      <Nuxt />
      <Footer />
    </div>
    
  </template>
  <script>
  import Header from "@/components/HeaderWeb"
  import Footer from "@/components/FooterWeb"
  export default {
    components:{
      Header,
      Footer
    }
  }
  </script>
  