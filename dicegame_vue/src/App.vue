<template>
  <div id="app">
    <div class="wrapper clearfix">
      <PlayerComponent
        v-bind:scorePlayer="scorePlayer"
        v-bind:activePlayer="activePlayer"
        v-bind:currentScore="currentScore"
        v-bind:isWinner="isWinner"
      />
      <ControlComponent
        v-on:handleNewGame="handleNewGame"
        v-on:handleRollDice="handleRollDice"
        v-on:handleHold="handleHold"
        v-bind:isPlaying="isPlaying"
        v-bind:finalScore="finalScore"
        v-on:handleChangeFinalScore="handleChangeFinalScore"
      />
      <DiceComponent v-bind:dices="dices" />
      <PopupRuleComponent
        v-bind:isOpenPopup="isOpenPopup"
        v-on:handleConfirm="handleConfirm"
      />
    </div>
  </div>
</template>

<script>
import PlayerComponent from "./Components/PlayerComponent.vue";
import ControlComponent from "./Components/ControlComponent.vue";
import DiceComponent from "./Components/DiceComponent.vue";
import PopupRuleComponent from "./Components/PopupRuleComponent.vue";
export default {
  name: "app",
  data() {
    return {
      isPlaying: false,
      isOpenPopup: false,
      activePlayer: 0, // 0:active đang chơi, 1: ngta chơi
      scorePlayer: [0, 0],
      dices: [1, 5],
      currentScore: 0,
      finalScore: ''
    };
  },
  components: {
    PlayerComponent,
    ControlComponent,
    DiceComponent,
    PopupRuleComponent,
  },
  computed: {
    isWinner() {
      let { scorePlayer, finalScore} = this;
      if(scorePlayer[0] >= finalScore || scorePlayer[1] >= finalScore) {
        // dừng cuôc chơi
        this.isPlaying = false;
        return true;
      }
      return false;
    }
  },
  methods: {
    handleConfirm() {
      this.isPlaying = true;
      this.isOpenPopup = false;
      this.activePlayer = 0;
      this.scorePlayer = [0, 0];
      this.dices = [1, 1];
      this.currentScore = 0;
    },
    handleNewGame() {
      this.isOpenPopup = true;
    },
    nextPlayer() {
      this.activePlayer = this.activePlayer == 0 ? 1 : 0; 
      this.currentScore = 0
    },
    handleRollDice() {
      if (this.isPlaying) {
        var dice1 = Math.floor(Math.random() * 6) + 1;
        var dice2 = Math.floor(Math.random() * 6) + 1;
        this.dices = [dice1, dice2];

        if (dice1 == 1 || dice2 == 1) {
          let activePlayer = this.activePlayer;
          // đổi lượt chơi
          setTimeout(function () {
            alert(`Người chơi Player ${activePlayer + 1} đã quay trúng số 1. Rất tiếc!`)
          }, 1000)
          this.nextPlayer()
        } else {
          this.currentScore = this.currentScore + dice1 + dice2;
        }
      } else {
        alert("Vui long chon new game");
      }
    },
    handleHold() { 
      if(this.isPlaying) { 
        let { scorePlayer, activePlayer, currentScore } = this
        this.$set(this.scorePlayer, activePlayer, scorePlayer[activePlayer] + currentScore)
        // let cloneScorePlayer = [...scorePlayer];
        //   cloneScorePlayer[activePlayer] = scorePlayer[activePlayer] + currentScore

        // // this.scorePlayer[activePlayer] = scorePlayer[activePlayer] + currentScore
        // this.scorePlayer = cloneScorePlayer 
        if(!this.isWinner) {
          this.nextPlayer()
        }
      }else {
        alert("Vui long chon new game");
      }
    },
    handleChangeFinalScore(event) { 
      var number = parseInt(event.target.value)
      if(isNaN(number)) {
        this.finalScore = ''
      } else {
        this.finalScore = number
      }
    }
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

body {
  background-image: linear-gradient(
      rgba(62, 20, 20, 0.4),
      rgba(62, 20, 20, 0.4)
    ),
    url("/public/assets/back.jpg");
  background-size: cover;
  background-position: center;
  font-family: Lato;
  font-weight: 300;
  position: relative;
  height: 100vh;
  color: #555;
}

.wrapper {
  width: 1000px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
  overflow: hidden;
}
</style>
