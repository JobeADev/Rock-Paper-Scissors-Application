<template>
  <div>
    <main v-if="isGameOver === false">
        <span id="score-box">
            <p>{{playerScore}}</p>
            <div id="divider">-</div>
            <p>{{computerScore}}</p>
        </span>
        <h1>Select an Option Below</h1>
        <span id="hand-icons">
            <img class="hands" src="../images/Rock.jpg" alt="Rock" @click="selectHand('Rock')" />
            <img class="hands" src="../images/Paper.jpg" alt="Paper" @click="selectHand('Paper')" />
            <img class="hands" src="../images/Scissors.jpg" alt="Scissors" @click="selectHand('Scissors')" />
        </span>
        <table id="results-table" v-show="playerChoice != ''">
          <thead>
            <tr>
              <td class="player-choice">You chose <p class="choice-name">{{ playerChoice }}</p></td>
              <td class="computer-choice">Computer chose <p class="choice-name">{{ computerChoice }}</p></td>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>
                <img v-show="playerChoice === 'Rock'" src="../images/Rock.jpg" alt="Rock" />
                <img v-show="playerChoice === 'Paper'" src="../images/Paper.jpg" alt="Paper" />
                <img v-show="playerChoice === 'Scissors'" src="../images/Scissors.jpg" alt="Scissors" />
              </td>
              <td>
                <img v-show="computerChoice === 'Rock'" src="../images/Rock.jpg" alt="Rock" />
                <img v-show="computerChoice === 'Paper'" src="../images/Paper.jpg" alt="Paper" />
                <img v-show="computerChoice === 'Scissors'" src="../images/Scissors.jpg" alt="Scissors" />
              </td>
            </tr>
          </tbody>
        </table>
        <h2>{{ matchMessage }}</h2>
    </main>
    <section v-else>
      <h1>{{ matchMessage }}</h1>
      <h2>Try Again? <a @click="resetGame">YES</a> | <router-link id="home-link" @click="this.$store.commit('CLEAR_MODE')" v-bind:to="{ name: 'home' }" >NO</router-link></h2>
    </section>
  </div>
</template>

<script>
// import MatchCompleteScreen from '../components/MatchCompleteScreen.vue';

export default {
  // components: { MatchCompleteScreen },
  data() {
    return {
      gameMode: '',
      playerChoice: '',
      computerChoice: '',
      matchMessage: '',
      playerScore: 0,
      computerScore: 0,
      isGameOver: false,
    }
  },
  methods: {
    selectHand(hand) {
      this.playerChoice = hand;
      this.computerChoice = this.generateComputerHand();
      this.determineWinner();
      if (this.gameMode != 3) { this.matchCheck() }
    },
    generateComputerHand() {
      const hands = ['Rock', 'Paper', 'Scissors'];
      return hands[Math.floor(Math.random() * hands.length)];
    },
    determineWinner() {
      if (this.playerChoice === this.computerChoice) {
        this.matchMessage = 'It\'s a tie!';
      } else if (
        (this.playerChoice === 'Rock' && this.computerChoice === 'Scissors') ||
        (this.playerChoice === 'Paper' && this.computerChoice === 'Rock') ||
        (this.playerChoice === 'Scissors' && this.computerChoice === 'Paper')
      ) {
        this.matchMessage = 'You win!';
        this.playerScore++;
      } else {
        this.matchMessage = 'You lose!';
        this.computerScore++;
      }
    },
    matchCheck() {
        if (this.gameMode === 1 && this.playerScore === 2) {
            this.matchMessage = 'You\'ve won the match!';
            this.isGameOver = true;
        } else if (this.gameMode === 1 && this.computerScore === 2) {
            this.matchMessage = 'You\'ve lost the match!';
            this.isGameOver = true;
        }

        if (this.gameMode === 2 && this.playerScore === 3) {
            this.matchMessage = 'You win the game!';
            this.isGameOver = true;
        } else if (this.gameMode === 2 && this.computerScore === 3) {
            this.matchMessage = 'You lost the match!';
            this.isGameOver = true;
        }
    },
    resetGame() {
      this.playerChoice = '';
      this.computerChoice = '';
      this.matchMessage = '';
      this.playerScore = 0;
      this.computerScore = 0;
      this.isGameOver = false;
    },
  },
  created() {
    this.gameMode = parseInt(localStorage.getItem('mode'));
    this.$store.commit('SET_MODE', this.gameMode);
  },
  beforeUpdate() {
    if (this.$store.state.previousMode) {
      if (this.$store.state.previousMode === this.$store.state.modeSelected) {
        this.gameMode = this.$store.state.previousMode
      }
    }
  }  
}
</script>

<style scoped>

main, section, #hand-icons, #results-table tr {
    display: flex;
}

main, section {
    flex-direction: column;
    align-items: center;
    height: 100vh;
    background-color: black;
    color: white;
    border-bottom: solid 3px rgba(255, 0, 0, 0.534);
}

#hand-icons {
    justify-content: space-around;
    width: 30%;
    margin-bottom: 8em;
}

img {
    width: 100px;
    height: 100px;
    transition: .6s;
    border: solid 3px rgba(255, 0, 0, 0.534);
}

.hands {
    transition: .6s;
}

.hands:hover {
    transform: scale(1.05);
    cursor: pointer;
}

#score-box {
    display: flex;
    font-size: 1.8em;
    margin-bottom: 1em;
    border-bottom: solid 3px rgba(255, 0, 0, 0.534);
    width: 12%;
    justify-content: space-between;
}

#score-box p {
    font-size: 1.6em;
    font-weight: bold;
    width: 100%;
    text-align: center;
    margin: 20px 0px 5px 0px;
}

#divider {
    font-size: 2em;
    margin-top: 5px;
}

table {
    width: 28%;
}

#results-table tr {
    justify-content: space-between;
    width: 100%;
}

.choice-name {
    font-weight: bold;
    color: rgba(255, 0, 0, 0.534);
    display: inline
}

a { 
  text-decoration: none;
  color: white;
  font-size: 1em;
  transition: color 0.4s;
}

a:hover {
  color: rgba(255, 0, 0, 0.534);
  cursor: pointer;
}

.player-choice, .computer-choice {
  margin-bottom: 5px;
}

</style>