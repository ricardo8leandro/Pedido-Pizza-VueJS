<template>
  <div>
    <Banner />
    <div class="main-container">
      <h1>Monte sua Pizza</h1>
      <PizzaForm />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import PizzaForm from '@/components/PizzaForm.vue';
import Banner from '@/components/Banner.vue';
export default {
  name: 'HomeView',
  components: {
    Banner,
    PizzaForm
  }
}
</script>
