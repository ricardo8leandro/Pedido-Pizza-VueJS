<template>
  <div>
    <NavBar :logo="logo_src" :alt="app_name"/>
    <router-view/>
    <Footer />
  </div>
</template>
<script>
import NavBar from '@/components/NavBar.vue';
import Footer from './components/Footer.vue';
export default {
  name: 'App',
  components: {
    NavBar,
    Footer
  },
  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Monte sua Pizza"
    }
  }
}
</script>
<style>
* {
  font-family: Helvetica;
  margin:0;
  padding: 0;
  box-sizing: border-box;
}

.main-container {
  margin:50px;
  min-height: 250px;
}

h1 {
  font-size: 42px;
  text-align: center;
  margin-bottom: 30px;
  color:#222;
}
</style>
