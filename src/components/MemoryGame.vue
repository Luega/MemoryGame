<template>
  <!-- CONTAINER -->
  <div class="container">
    <!-- TOP -->
    <!-- TITLE -->
    <div class="container_top">
      <div>
        <h1>Lele and Bea's Memory </h1>
      </div>
      <!-- SELECTION OF THE LEVEL -->
      <div class="choiceBox">
        <!-- the user will select the player and this will select the starting array (dog or croc) -->
        <select class="choiceBox_select" v-model="player">
          <option :value="null" disabled hidden>Player</option>
          <option v-for="(player, keyb) in players" :key="keyb" :value="player.value">
            {{ player.text }}
          </option>
        </select>
        <!-- the user will select the level from an array that will set the number of the cards -->
        <select class="choiceBox_select" v-model="cardsNumber">
          <option :value="null" disabled hidden>Level</option>
          <option v-for="(level, keya) in levels" :key="keya" :value="level.value">
            {{ level.text }}
          </option>
        </select>
        <!-- Clicking the button, the cards will be shown on the playgound with the number of cards related to the choosen level -->
        <button class="choiceBox_button" @click="createRandomArray()">PLAY</button>
      </div>
    </div>
    <!-- BOTTOM -->
    <div>
      <!-- PLAYGROUND -->
      <div class="container_bottom">
        <!-- CARDS -->
        <!-- run a v-for on the gamingCardArray to show cards and added the click event -->
        <div :id="`card-${key}`" class="card" tabindex="0" v-for="(card, key) in gamingCardsArray" :key="key" @click="selectCard(card, key)" @keyup.enter="selectCard(card, key)">
          <img class="card_img" :id="`ab-${key}`" :src="require(`@/assets/img/${card.img}`)" alt="Card-img">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MemoryGame',
  data() {
    return {
      // choosed number of cards in the game 
      cardsNumber: null,
      // choosed number who will play the game 
      player: null,
      // option for the player input
      players: [
        { text: 'Lele', value: 'lele' },
        { text: 'Bea', value: 'bea' }
      ],
      // option for the level input
      levels: [
        { text: 'Easy', value: '6' },
        { text: 'Normal', value: '12' },
        { text: 'Hard', value: '18' },
        { text: 'Hero', value: '24' }
      ],
      // array for the imgs comparison
      comparisonArray: [],
      // array of img ids to change the display mode of the imgs if the imgs selected are not the same
      idArray: [],
      // array for the ending of the game
      endingArray: [],
      // array for the gaming cards
      gamingCardsArray: [],
      // array for all the cards
      crocodilesArray: [
        {
          img: "croc1.jpg",
          selected: false,
        },
        {
          img: "croc1.jpg",
          selected: false,
        },
        {
          img: "croc2.png",
          selected: false,
        },
        {
          img: "croc2.png",
          selected: false,
        },
        {
          img: "croc3.jpg",
          selected: false,
        },
        {
          img: "croc3.jpg",
          selected: false,
        },
        {
          img: "croc4.jpg",
          selected: false,
        },
        {
          img: "croc4.jpg",
          selected: false,
        },
        {
          img: "croc5.jpg",
          selected: false,
        },
        {
          img: "croc5.jpg",
          selected: false,
        },
        {
          img: "croc6.jpg",
          selected: false,
        },
        {
          img: "croc6.jpg",
          selected: false,
        },
        {
          img: "croc7.jpg",
          selected: false,
        },
        {
          img: "croc7.jpg",
          selected: false,
        },
        {
          img: "croc8.jpg",
          selected: false,
        },
        {
          img: "croc8.jpg",
          selected: false,
        },
        {
          img: "croc9.jpg",
          selected: false,
        },
        {
          img: "croc9.jpg",
          selected: false,
        },
        {
          img: "croc10.jpg",
          selected: false,
        },
        {
          img: "croc10.jpg",
          selected: false,
        },
        {
          img: "croc11.jpg",
          selected: false,
        },
        {
          img: "croc11.jpg",
          selected: false,
        },
        {
          img: "croc12.jpg",
          selected: false,
        },
        {
          img: "croc12.jpg",
          selected: false,
        }
      ],
      dogsArray: [
        {
          img: "dog1.jpg",
          selected: false,
        },
        {
          img: "dog1.jpg",
          selected: false,
        },
        {
          img: "dog2.jpg",
          selected: false,
        },
        {
          img: "dog2.jpg",
          selected: false,
        },
        {
          img: "dog3.jpeg",
          selected: false,
        },
        {
          img: "dog3.jpeg",
          selected: false,
        },
        {
          img: "dog4.jpg",
          selected: false,
        },
        {
          img: "dog4.jpg",
          selected: false,
        },
        {
          img: "dog5.png",
          selected: false,
        },
        {
          img: "dog5.png",
          selected: false,
        },
        {
          img: "dog6.jpg",
          selected: false,
        },
        {
          img: "dog6.jpg",
          selected: false,
        },
        {
          img: "dog7.jpg",
          selected: false,
        },
        {
          img: "dog7.jpg",
          selected: false,
        },
        {
          img: "dog8.jpg",
          selected: false,
        },
        {
          img: "dog8.jpg",
          selected: false,
        },
        {
          img: "dog9.png",
          selected: false,
        },
        {
          img: "dog9.png",
          selected: false,
        },
        {
          img: "dog10.jpg",
          selected: false,
        },
        {
          img: "dog10.jpg",
          selected: false,
        },
        {
          img: "dog11.jpg",
          selected: false,
        },
        {
          img: "dog11.jpg",
          selected: false,
        },
        {
          img: "dog12.jpg",
          selected: false,
        },
        {
          img: "dog12.jpg",
          selected: false,
        },
      ]
    }
  },
  beforeMount () {
    // add the cardsNumber value and player value in local storage to the cardsNumber value (for the end of the game) and player in data
    this.player = localStorage.getItem('player');
    this.cardsNumber = localStorage.getItem('cardsNumber');
    //create the gamingCardsArray with the number of cards and for the player that are stored in the local storage (to show the cards immediately)
    // use the crocodile array if lele is the player
    if (this.player == 'lele') {
      // for loop to create, from the crocodilesArray, the gamingCardsArray with the right number of cards related with the choosen level 
      for (let i = 0; i < this.cardsNumber; i++) {
        this.gamingCardsArray.push(this.crocodilesArray[i]);
      }
      // get random the elements in the array
      this.gamingCardsArray = this.gamingCardsArray.sort(() => 0.5 - Math.random());
      // clear the HTML bottom container from crocodile welcome
      document.querySelector('.container_bottom').innerHTML = '';
    } else if (this.player == 'bea') {
      // for loop to create, from the dogsArray, the gamingCardsArray with the right number of cards related with the choosen level 
      for (let i = 0; i < this.cardsNumber; i++) {
        this.gamingCardsArray.push(this.dogsArray[i]);
      }
      // get random the elements in the array
      this.gamingCardsArray = this.gamingCardsArray.sort(() => 0.5 - Math.random());
      // clear the HTML bottom container from crocodile welcome
      document.querySelector('.container_bottom').innerHTML = '';
    }
  },
  mounted () {
    // if localStorage is null it will show the welcome crocodile in the bottom container
    if (localStorage.getItem('cardsNumber') === null) {
      this.showStartingCroc();
    }
  },
  methods: {
    selectCard(card, key) {
      // if the selected value of the card is false
      if (card.selected == false) {
        // change selected value of the card 
        card.selected = true; 
        // change the display mode of the card's img
        document.getElementById(`ab-${key}`).style.display = "inline";
        // push the id of the img in the ids array
        this.idArray.push(`ab-${key}`);
        // push the obj in the comparison array
        this.comparisonArray.push(card);
        // after the second card selection
        if (this.comparisonArray.length == 2) {
          // if the img of objs are the same
          if (this.comparisonArray[0].img == this.comparisonArray[1].img) {
            // push objs of comparisonArray in to endingArray
            this.endingArray.push(this.comparisonArray[0], this.comparisonArray[1]);
            // remove the objts from comparisonArray
            this.comparisonArray.splice(0, 2);
            // remove the ids from idsArray
            this.idArray.splice(0, 2);
            // if the number of obj in the endingArray is the same of the cardsNumber the game is ended and ending-crocodile will be shown
            if (this.endingArray.length == this.cardsNumber) {
              setTimeout(() => {
                this.showEndingCroc();
              }, 1000);
            }
            // if the img of objs are not the same
          } else if (this.comparisonArray[0].img !== this.comparisonArray[1].img) { 
            // set a timeout to see the second card selected
            setTimeout(() => {
              // change the display imgs of both selected cards to none
              document.getElementById(this.idArray[0]).style.display = "none";
              document.getElementById(this.idArray[1]).style.display = "none";
              // remove the ids from idArray
              this.idArray.splice(0, 2);
            }, 1000);
            // change the card selected value to false
            this.gamingCardsArray.forEach(obj => {
              if (this.comparisonArray.includes(obj)) {
                obj.selected = false;
              }
            });
            // remove the objts from comparisonArray
            this.comparisonArray.splice(0, 2);
          }
        }
      // if the selected value of the card is true
      } else {
        // if the card is not already matched
        if (!this.endingArray.includes(card)) {
          // remove the objts from comparisonArray
          this.comparisonArray.splice(0, 1);
          // remove the id from idArray
          this.idArray.splice(0, 1);
          // change the card selected value in false
          card.selected = false;
          // change the card img display mode in none
          document.getElementById(`ab-${key}`).style.display = "none";
        // if the card is already matched
        } else {
          document.getElementById(`card-${key}`).classList.add('cardAlreadySelected');
          setTimeout(() => {
            document.getElementById(`card-${key}`).classList.remove('cardAlreadySelected');
          }, 1500);
        }
      }
    },
    createRandomArray() {
      // if in local storage there isn't cardsNumber stored 
      if (localStorage.getItem('cardsNumber') === null) {
        // set the cardsNumber value in the data with the value of the first choice and the first player (it will start with the basic level and first player)
        if (this.player == null && this.level == null) {
          this.player = this.players[0].value;
          this.cardsNumber = this.levels[0].value;
        // if there isn't the player value  
        } else if (this.player == null) {
          this.player = this.players[0].value;
        // if there isn't the level value  
        } else if (this.level == null) {
          this.cardsNumber = this.levels[0].value;
        }
        // set in local Storage the player
        localStorage.setItem('player', this.player);
        // set in local Storage the cards Number
        localStorage.setItem('cardsNumber', this.cardsNumber);
        // use the crocodile array if lele is the player
        if (this.player == 'lele') {
          // for loop to create, from the crocodilesArray, the gamingCardsArray with the right number of cards related with the choosen level 
          for (let i = 0; i < this.cardsNumber; i++) {
            this.gamingCardsArray.push(this.crocodilesArray[i]);
          }
          // get random the elements in the array
          this.gamingCardsArray = this.gamingCardsArray.sort(() => 0.5 - Math.random());
          // clear the HTML bottom container from crocodile welcome
          document.querySelector('.container_bottom').innerHTML = '';
        } else if (this.player == 'bea') {
          // for loop to create, from the dogsArray, the gamingCardsArray with the right number of cards related with the choosen level 
          for (let i = 0; i < this.cardsNumber; i++) {
            this.gamingCardsArray.push(this.dogsArray[i]);
          }
          // get random the elements in the array
          this.gamingCardsArray = this.gamingCardsArray.sort(() => 0.5 - Math.random());
          // clear the HTML bottom container from crocodile welcome
          document.querySelector('.container_bottom').innerHTML = '';
        }
      // if in local storage there is cardsNumber stored (this means that we want to change level)
      } else {
        // clear the localStorage from the old cardsNumber value
        localStorage.clear();
        // add the new cardsNumber Value and player in the localStorage
        localStorage.setItem('cardsNumber', this.cardsNumber);
        localStorage.setItem('player', this.player);
        // reload the page (the new cardsNumber in localStorage will be used beforeMount)
        location.reload();
      }
    },
    // function to show in bottom container the crocodile animation if the player have win
    showEndingCroc() {
      document.querySelector('.container_bottom').innerHTML = 
      ` 
      <div class="box-end">
        <h1 class="text-crocodile">you win</h1>
        <div class="head">
          <div class="eye-left"></div>
          <div class="eye-right"></div>
          <div class="mouth"></div>
          <div class="tooth"></div>
          <div class="cheek"></div>
          <div class="cheek-copy"></div>
          <div class="nose">
            <div class="nose-hole-left"></div>
            <div class="nose-hole-right"></div>
          </div>
        </div>
        <div class="body">
          <div class="belly">
            <div class="stripes"></div>
          </div>
        </div>
        <div class="body-copy">
          <div class="fur-top"></div>
          <div class="fur-middle"></div>
          <div class="fur-bottom"></div>
        </div>
        <div class="hat-container">
          <div class="hat-base">
            <div class="hat-ribbon"></div>
          </div>
          <div class="hat-bottom"></div>
          <div class="hat-feather-top"></div>
          <div class="hat-feather-bottom"></div>
        </div>
      </div>
      `;
    },
    // function to show in bottom container the welcome crocodile css/html
    showStartingCroc() {
      document.querySelector('.container_bottom').innerHTML = 
      ` 
      <div class="box-start">
        <h1 class="text-crocodile">welcome</h1>
        <div class="head">
          <div class="eye-left"></div>
          <div class="eye-right"></div>
          <div class="mouth"></div>
          <div class="tooth"></div>
          <div class="cheek"></div>
          <div class="cheek-copy"></div>
          <div class="nose">
            <div class="nose-hole-left"></div>
            <div class="nose-hole-right"></div>
          </div>
        </div>
        <div class="body">
          <div class="belly">
            <div class="stripes"></div>
          </div>
        </div>
        <div class="body-copy">
          <div class="fur-top"></div>
          <div class="fur-middle"></div>
          <div class="fur-bottom"></div>
        </div>
        <div class="hat-container">
          <div class="hat-base">
            <div class="hat-ribbon"></div>
          </div>
          <div class="hat-bottom"></div>
          <div class="hat-feather-top"></div>
          <div class="hat-feather-bottom"></div>
        </div>
      </div>
      `;
    },
  }
}
</script>

<style lang="scss">
// CONTAINER
.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: #F2F5C8;
}
// TOP
.container_top {
  width: 70%;
  margin: 1rem auto 1rem auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #F2F5C8;
}
.container_top h1 {
  margin-bottom: 2rem;
  padding: 0.5rem 3rem;
  color: black;
  text-transform: uppercase;
  background-color:#C1DEAE;
  box-shadow: 5px 5px 2px #219F94;
}
.container_top .choiceBox {
  width: 100%;
  display: flex;
  justify-content: center;
}
// SELECT
.choiceBox_select {
  margin-right: 4rem;
  padding: 0.5rem;
  color: black;
  font-size: larger;
  font-weight: bolder;
  background-color: #C1DEAE;
  border: none;
  box-shadow: 5px 5px 2px #219F94;
  transition-duration: 0.5s;
  transition-property: transform;
  outline: none;
  cursor: pointer;
}
.choiceBox_select:hover,
.choiceBox_select:active,
.choiceBox_select:focus {
  transform: scale(1.1);
}
// BUTTON
.choiceBox_button {
  padding: 0.5rem 1.5rem;
  color: black;
  font-size: large;
  font-weight: bold;
  background-color: #C1DEAE;
  border: none;
  box-shadow: 5px 5px 2px #219F94;
  transition-duration: 0.5s;
  transition-property: transform;
  outline: none;
  cursor: pointer;
}
.choiceBox_button:hover {
  transform: rotate(20deg) scale(1.1);
}
.choiceBox_button:active,
.choiceBox_button:focus {
  transform: scale(1.1);
}
// BOTTOM
.container_bottom {
  width: 85%;
  min-height: 30vh;
  margin: 1rem auto 0 auto;
  background-color: #F2F5C8;
  border-top: 1px dotted black;
  border-bottom: 1px dotted black;
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}
// CARD
.container_bottom .card {
  flex-basis: calc((100% / 6) - 30px);
  height: 100px;
  margin: 15px;
  background-color: #219F94;
  border-radius: 10px;
  box-shadow: 5px 5px 2px #C1DEAE;
  overflow: hidden;
  transition-duration: 0.5s;
  transition-property: transform;
  outline: none;
  cursor: pointer;
}
.container_bottom .card:active,
.container_bottom .card:focus,
.container_bottom .card:hover {  
  transform: scale(1.1);
}
.container_bottom .cardAlreadySelected {
  animation: already-selected 0.075s infinite alternate; 
}
.card_img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  display: none;
}

// ENDING CROCODILE
.box-start,
.box-end {
  position: relative;
  margin: 1rem auto;
  width: 600px;
  height: 420px;
  background: none;
  border: solid 3px white; 
  background: #F0F3AE;
  border: 3px solid #4F3130;
}
.box-end {
  animation: ending-croc 5s;
}
.text-crocodile {
  margin: 0.3rem 4rem 0 4rem;
  padding: 0.5rem 3rem;
  color: black;
  text-align: center;
  text-transform: uppercase;
  background-color:#C1DEAE;
  box-shadow: 0 5px 2px #219F94;
}
.head{
  position:absolute;
  background: #A8B956;
  width: 25%;
  height: 17%;
  top: 35%;
  left: 30%;
  border-bottom-left-radius: 15px;
  z-index:1;
}
.mouth{
  position:absolute;
  width: 110px;
  height: 2px;
  background: #422218;
  top: 55%;
}
.tooth{
  position:absolute;
  width: 8%;
  height: 22%;
  background: #fff;
  -webkit-clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
  clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
  top:33%;
  left: 30%;
}
.cheek{
  position:absolute;
  width: 18%;
  height: 36%;
  background: tomato;
  border-radius: 50%;
  top:37%;
  right: 16%;
}
.eye-right{
  position:absolute;
  width: 6%;
  height: 12%;
  background: #422218;
  border-radius:50%;
  top: 20%;
  right: 3%;
}
.eye-left{
  position:absolute;
  width: 6%;
  height: 12%;
  background: #422218;
  border-radius:50%;
  top: 12%;
  right: 20%;
}
.nose{
  position:absolute;
  width: 27%;
  height: 40%;
  background: #A8B956;
  top: -25%;
}
.nose-hole-left{
  position:absolute;
  background: #422218;
  width:15%;
  height: 60%;
  border-radius: 50%;
  top:30%;
  left:20%;
}
.nose-hole-right{
  position:absolute;
  background: #422218;
  width:15%;
  height: 60%;
  border-radius: 50%;
  top:30%;
  right:20%;
}
.body{
  position:absolute;
  background: #A8B956;
  width: 20%;
  height: 60%;
  top: 35%;
  left: 40%;  
  -webkit-clip-path: polygon(20% 0%, 80% 0%, 100% 100%, 0% 100%);
  clip-path: polygon(20% 0%, 80% 0%, 100% 100%, 0% 100%);
}
.body-copy{
  position:absolute;
  background: #F0F3AE;
  width: 20%;
  height: 60%;
  top: 35%;
  left: 56%; 
}
.fur-top{
  position:absolute;
  background: #879E2D;
  width: 50%;
  height: 25%;
  top: 20%;
  -webkit-clip-path: polygon(100% 50%, 0 0, 0 100%);
  clip-path: polygon(100% 50%, 0 0, 0 100%);
   z-index:1;
}
.fur-middle{
  position:absolute;
  background: #879E2D;
  width: 50%;
  height: 25%;
  top: 45%;
  -webkit-clip-path: polygon(100% 50%, 0 0, 0 100%);
  clip-path: polygon(100% 50%, 0 0, 0 100%);
   z-index:1;
}
.fur-bottom{
  position:absolute;
  background: #879E2D;
  width: 50%;
  height: 25%;
  bottom: 5%;
  -webkit-clip-path: polygon(100% 50%, 0 0, 0 100%);
  clip-path: polygon(100% 50%, 0 0, 0 100%);
   z-index:1;
}
.hat-container{
  position:absolute;
  background:none;
  height:20%;
  width:10%;
  right:40%;
  top:14%;
}
.hat-base{
  position:absolute;
  background: #4F3130;
  height: 70%;
  width: 70%; 
  top:10%;
  left:15%;
  border-top-left-radius: 50px;
  border-top-right-radius: 50px;
}
.hat-ribbon{
  position:absolute;
  background: white;
  height: 15%;
  width:100%;
  bottom:0;
  z-index:1;
}
.hat-bottom{
  position:absolute;
  background:#4F3130;
  height: 14%;
  width:100%;
  bottom:6%;
}
.hat-feather-top{
  position:absolute;
  background: #AA5042;
  height:55%;
  width:50%;
  -webkit-clip-path: polygon(25% 0, 75% 0, 61% 100%, 36% 100%);
  clip-path: polygon(25% 0, 75% 0, 61% 100%, 36% 100%);
  border-top-left-radius: 90px;
  border-top-right-radius: 90px;
  top: 20%;
  right:-7%;
  transform: rotate(20deg);
}
.hat-feather-bottom{
  position:absolute;
  background:#D8BD8A;
  height:45%;
  width:40%;
  -webkit-clip-path: polygon(25% 0, 75% 0, 61% 100%, 36% 100%);
  clip-path: polygon(25% 0, 75% 0, 61% 100%, 36% 100%);
  border-top-left-radius: 90px;
  border-top-right-radius: 90px;
  top: 33%;
  right:-10%;
  transform: rotate(40deg);
}
.belly{
  position:absolute;
  top:25%;
  left:-35%;
  width: 100%;
  height: 80%;
  -webkit-clip-path: ellipse(16% 40% at 50% 50%);
  clip-path: ellipse(16% 40% at 50% 50%);
  transform: rotate(5deg);
}
.stripes{
  height:100%;
  width:100%;
  background: linear-gradient(
  to bottom,
  #BCCC61,
  #BCCC61 50%,
  #879E2D 50%,
  #879E2D
  );
  background-size: 100% 10px;
}
// ANIMATION
//animation for ending-crocodile
@keyframes ending-croc {
  0% {
    transform: scale(0);
  }
  10% {
    transform: scale(1.1);
  }
  20% {
    transform: scale(0.8);
  }
  30% {
    transform: scale(1.1);
  }
  60% {
    transform: scale(1);
  }
}
//animation for already selected card
@keyframes already-selected {
  from {
    transform: scale(1.1) translateX(-3px);
  }
  to {
    transform: scale(1.1) translateX(3px);
  }
}
// MEDIAQUERY
@media only screen and (min-width: 1600px) {
  .container_top {
    width: 45%;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
  }
  .container_top h1 {
    margin-right: 4rem;
  }
  .container_bottom {
    width: 45%;
  }
}
@media only screen and (max-width: 700px) {
  .container_bottom .card {
    flex-basis: calc((100% / 3) - 30px);
  }
  .box-start,
  .box-end {
    width: 500px;
    height: 320px;
  }
  .mouth {
    width: 90px;
  }
}
@media only screen and (max-width: 600px) {
  .container_bottom .card {
    flex-basis: calc((100% / 2) - 30px);
  }
  .container_top .choiceBox {
    flex-wrap: wrap;
    flex-direction: column;
    align-items: center;
  }
  .container_top .choiceBox_select {
    margin: 0 0 1rem 0;
  }
  .box-start,
  .box-end {
    width: 400px;
    height: 220px;
  }
  .text-crocodile {
    font-size: large;
  }
  .mouth {
    width: 70px;
  }
}
@media only screen and (max-width: 420px) {
  .box-start,
  .box-end {
    width: 300px;
    height: 120px;
  }
  .text-crocodile {
    font-size: small;
    margin: 0 4rem 0 4rem;
    padding: 0.2rem;
  }
  .mouth {
    width: 50px;
  }
}
</style>
