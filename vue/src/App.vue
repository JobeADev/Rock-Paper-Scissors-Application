<template>
  <main id="vue-app">
    <site-banner />
    <router-view />
  </main>
</template>

<script>
import SiteBanner from './components/SiteBanner.vue';

export default {
  components: { SiteBanner },
  data() {
    return {
    }
  }
}
</script>

<style scoped>

</style>
