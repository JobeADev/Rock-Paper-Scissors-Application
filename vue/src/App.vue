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
  methods: {
    setMode(mode) {
      this.$store.commit('SET_MODE', mode);
    },
    clearMode() {
      this.$store.commit('CLEAR_MODE');
    },
    handlePopstate(e) {
      if (this.$route.path === '/') {
        this.$store.commit('SET_PREVIOUS_MODE', this.$store.state.modeSelected)
        this.previousMode = this.$store.state.modeSelected
        this.clearMode();
      } else {
        this.setMode(this.previousMode)
      }
    }
  },
  data() {
    return {
      previousMode: '',
    }
  },
  created() {
    window.addEventListener("popstate", this.handlePopstate);
  },
}
</script>

<style>

body {
  margin: 0px 0px;
}

</style>
