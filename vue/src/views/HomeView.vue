<template>
    <main>
        <h1>Rock, Paper, Scissors</h1>
        <p>The rules are simple. Rock beats Scissors, Scissors beats Paper, and Paper beats Rock.</p>
        <p>Click on "BEST OF 3" to play a best of 3 game.</p>
        <p>Click on "BEST OF 5" to play a best of 5 game.</p>
        <p>Click on "ENDLESS" to play an endless game.</p>
    </main>
</template>

<script>
export default {

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

h1 {
    font-size: 2.5em;
    margin-bottom: 1em;
    border-bottom: solid 3px rgba(255, 0, 0, 0.534);
    /* text-shadow: 3px 3px 6px rgba(255, 0, 0, 0.534); */

}

p {
   text-shadow: 1px 1px 5px rgba(255, 0, 0, 0.534);
}

</style>