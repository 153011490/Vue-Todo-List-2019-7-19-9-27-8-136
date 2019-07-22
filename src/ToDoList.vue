<template>
    <body>
      <div id="app" class="container">
      <Header></Header>
      <Body ref="Body"></Body>
      <Footer @filter="filter"></Footer>
    </div>
    </body>
</template>

<script>
import Header from "./components/Header.vue";
import Body from "./components/Body.vue";
import Footer from "./components/Footer.vue";
export default {
  name: 'app',
  components:{
    Header,
    Body,
    Footer
  },
  methods:{
    filter(type){
      this.$refs.Body.changeType(type);
    }
  }
}
</script>

<style>
.container{
    padding: 20px;
    width: 500px;
    margin: 0 auto;
    margin-top: 40px;
    background: white;
}
body{
    background: #ccc;
}
</style>
