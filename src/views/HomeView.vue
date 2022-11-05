<template>
  <Banner />
  <div class="main-container">
  <h1>Make Your Burger:</h1>
  </div>
</template>

<script>
// @ is an alias to /src
import Banner from '@/components/Banner.vue';
export default {
  name: 'HomeView',
  components: {
    Banner
  }
}
</script>
