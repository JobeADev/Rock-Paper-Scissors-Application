<template>
  <nav>
    <router-link @click="clearMode" id="home-link" v-bind:to="{ name: 'home' }" ><img id="home-logo" src="../images/Logo.png"></router-link>
    <div id="space"></div>
    <router-link v-if="mode === ''" @click="setMode(1)" class="mode" v-bind:to="{ name: 'game' }" >BEST OF 3</router-link>
    <router-link v-if="mode === ''" @click="setMode(2)" class="mode" v-bind:to="{ name: 'game' }" >BEST OF 5</router-link>
    <router-link v-if="mode === ''" @click="setMode(3)" class="mode" v-bind:to="{ name: 'game' }" >ENDLESS</router-link>
    <p class="mode" v-if="mode === 1">BEST OF 3 MODE</p>
    <p class="mode" v-if="mode === 2">BEST OF 5 MODE</p>
    <p class="mode" v-if="mode === 3">ENDLESS MODE</p>
  </nav>
</template>

<script>
export default {
    methods: {
        setMode(mode) {
            this.$store.commit('SET_MODE', mode);
        },
        clearMode() {
            this.$store.commit('CLEAR_MODE');
        }
    },
    computed: {
        mode() {
            return this.$store.state.modeSelected;
        }
    },
}
</script>

<style scoped>

a {
    text-decoration: none;
    height: 60px;
    padding: 0px 12.5px 0px 12.5px;
    color: white;
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    font-size: 28px;
    transition: color 0.4s;
}

P {
    text-decoration: none;
    height: 60px;
    margin: 0px;
    padding: 0px 12.5px 0px 12.5px;
    color: white;
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    font-size: 28px;
}

a:first-of-type {
    padding-left: 0px;
}

a:hover {
    color: rgba(255, 0, 0, 0.534);
}

.mode {
    height: 50px;
    padding-top: 10px;
}

#home-logo {
    width: 80px;
    height: 60px;
}

nav {
    display: flex;
    /* justify-content: space-between; */
    padding: .8em;
    background-color: black;
    border-top: solid 3px rgba(255, 0, 0, 0.534);
    border-bottom: solid 3px rgba(255, 0, 0, 0.534);
}

#space {
    padding-right: 20px;
}

</style>