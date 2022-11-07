<template>
  <div class="main-container">
    <h1>Managments Requests:</h1>
      <Dashboard />
  </div>
</template>


<script>
  import Dashboard from '../components/Dashboard'

export default {
  name: 'RequestView',
  components: {
    Dashboard
  }
}
</script>
