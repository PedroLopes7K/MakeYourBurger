<template>
  
  <nav>

    <router-link to="/" id="logo_url">
      <img :src="logo" alt="Logo" id="logo">
    </router-link> 
    <router-link to="/">Home</router-link> 
    <router-link to="/request">Request</router-link>
  </nav>
</template>

<script>

export default {
  name: 'NavBar',
  props: ['logo'],
  components: {
  },
}
</script>

<style scoped>

nav {
  background-color: #222;
  border-bottom:  4px solid #111;
  padding: 15px 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
nav #logo_url {
  margin: auto;
  margin-left:0 ;
}
#logo {
  width: 40px;
  height: 40px;
}

nav a {
  color: #FCBA03;
  text-decoration: none;
  margin: 12px;
  translate: .5s;
}

nav a:hover {
  color: #fff;
}
</style>