<template>
  <main>
    <h1>{{ matchMessage }}</h1>
    <h2>Try Again? <a>YES</a> | <router-link id="home-link" @click="this.$store.commit('CLEAR_MODE')" v-bind:to="{ name: 'home' }" >NO</router-link></h2>
  </main>
</template>

<script>
export default {
  props: ['matchMessage'],
}
</script>

<style scoped>

main {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100vh;
    background-color: black;
    color: white;
    padding-top: 10em;
    border-bottom: solid 3px rgba(255, 0, 0, 0.534);
}

a { 
  text-decoration: none;
  color: white;
  font-size: 1em;
  transition: color 0.4s;
}

a:hover {
  color: rgba(255, 0, 0, 0.534);
}

</style>