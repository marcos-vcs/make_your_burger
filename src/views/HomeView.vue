<template>
  <Banner></Banner>
  <div class="main-container">
      <h1>Monte seu burger</h1>
      <BurgerForm></BurgerForm>
  </div>
</template>

<script>
import Banner from '@/components/Banner.vue';
import BurgerForm from '@/components/BurgerForm.vue';

  export default {
    name: 'HomeView',
    components: {
      Banner,
      BurgerForm,
    }
  }
</script>
