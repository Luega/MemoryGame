<template>
  <!-- CONTAINER -->
  <div class="container">
    <!-- TOP -->
    <!-- TITLE -->
    <div class="container_top">
      <div>
        <h1>Memory di Lele e Bea</h1>
      </div>
      <!-- SELECTION OF THE LEVEL -->
      <div class="choiceBox">
        <!-- the user will select the level from an array that will set the number of the cards -->
        <select class="choiceBox_select" v-model="cardsNumber">
          <option v-for="(level, keya) in levels" :key="keya" :value="level.value">
            {{ level.text }}
          </option>
        </select>
        <!-- Clicking the button, the cards will be shown on the playgound with the number of cards related to the choosen level -->
        <button class="choiceBox_button" @click="createRandomArray()">GIOCA</button>
      </div>
    </div>
    <!-- BOTTOM -->
    <div>
      <!-- PLAYGROUND -->
      <div class="container_bottom">
        <!-- CARDS -->
        <!-- run a v-for on the gamingCardArray to show cards and added the click event -->
        <div class="card" v-for="(croc, key) in gamingCardsArray" :key="key" @click="selectCard(croc, key)">
          <img class="card_img" :id="`ab-${key}`" :src="require(`@/assets/img/${croc.img}`)" alt="Croc">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BabboleoWorld',
  props: {
    
  },
  data() {
    return {
      // choosed number of cards in the game 
      cardsNumber: null,
      // option for the input
      levels: [
        { text: 'Luega', value: '6' },
        { text: 'Irene', value: '12' },
        { text: 'Alessio', value: '18' },
        { text: 'Marta', value: '24' }
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
          img: "cartoon-crocodile-vector-21277180.jpg",
          selected: false,
        },
        {
          img: "cartoon-crocodile-vector-21277180.jpg",
          selected: false,
        },
        {
          img: "posters-krokodil.jpg.jpg",
          selected: false,
        },
        {
          img: "posters-krokodil.jpg.jpg",
          selected: false,
        },
        {
          img: "gaetano-cessati-YOX8ZMTo7hk-unsplash.jpg",
          selected: false,
        },
        {
          img: "gaetano-cessati-YOX8ZMTo7hk-unsplash.jpg",
          selected: false,
        },
        {
          img: "jack-kelly-gAvQfrHwbgY-unsplash.jpg",
          selected: false,
        },
        {
          img: "jack-kelly-gAvQfrHwbgY-unsplash.jpg",
          selected: false,
        },
        {
          img: "lisa-yount-POKb4uUOizU-unsplash.jpg",
          selected: false,
        },
        {
          img: "lisa-yount-POKb4uUOizU-unsplash.jpg",
          selected: false,
        },
        {
          img: "rae-wallis-0P0_fMu-XFs-unsplash.jpg",
          selected: false,
        },
        {
          img: "rae-wallis-0P0_fMu-XFs-unsplash.jpg",
          selected: false,
        },
        {
          img: "shelly-collins-YppMBEPyfFQ-unsplash.jpg",
          selected: false,
        },
        {
          img: "shelly-collins-YppMBEPyfFQ-unsplash.jpg",
          selected: false,
        },
        {
          img: "simon-watkinson-qdg2Hxyjz4M-unsplash.jpg",
          selected: false,
        },
        {
          img: "simon-watkinson-qdg2Hxyjz4M-unsplash.jpg",
          selected: false,
        },
        {
          img: "simon-watkinson-qdg2Hxyjz4M-unsplash.jpg",
          selected: false,
        },
        {
          img: "simon-watkinson-qdg2Hxyjz4M-unsplash.jpg",
          selected: false,
        },
        {
          img: "simon-watkinson-qdg2Hxyjz4M-unsplash.jpg",
          selected: false,
        },
        {
          img: "simon-watkinson-qdg2Hxyjz4M-unsplash.jpg",
          selected: false,
        },
        {
          img: "simon-watkinson-qdg2Hxyjz4M-unsplash.jpg",
          selected: false,
        },
        {
          img: "simon-watkinson-qdg2Hxyjz4M-unsplash.jpg",
          selected: false,
        },
        {
          img: "simon-watkinson-qdg2Hxyjz4M-unsplash.jpg",
          selected: false,
        },
        {
          img: "simon-watkinson-qdg2Hxyjz4M-unsplash.jpg",
          selected: false,
        }
      ]
    }
  },
  beforeMount () {
    // add the cardsNumber value in local storage to the cardsNumber value in data (for the end of the game)
    this.cardsNumber = localStorage.getItem('cardsNumber');
    //create the gamingCardsArray with the number of cards that are stored in the local storage (to show the cards immediately)
    for (let i = 0; i < localStorage.getItem('cardsNumber'); i++) {
      this.gamingCardsArray.push(this.crocodilesArray[i]);
    }
    // get random the elements in the array
    this.gamingCardsArray = this.gamingCardsArray.sort(() => 0.5 - Math.random());
  },
  methods: {
    selectCard(croc, key) {
      // if the selected value of the card is false
      if (croc.selected == false) {
        // change selected value of the card 
        croc.selected = true; 
        // change the display mode of the card's img
        document.getElementById(`ab-${key}`).style.display = "inline";
        // push the id of the img in the ids array
        this.idArray.push(`ab-${key}`);
        // push the obj in the comparison array
        this.comparisonArray.push(croc);
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
            // if the number of obj in the endingArray is the same of the cardsNumber the game is ended
            if (this.endingArray.length == this.cardsNumber) {
              setTimeout(() => {
                alert('hai vinto!')
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
        if (!this.endingArray.includes(croc)) {
          // remove the objts from comparisonArray
          this.comparisonArray.splice(0, 1);
          // remove the id from idArray
          this.idArray.splice(0, 1);
          // change the card selected value in false
          croc.selected = false;
          // change the card img display mode in none
          document.getElementById(`ab-${key}`).style.display = "none";
        } else {
          alert('Hai giá indovinato questa carta');
        }
      }
    },
    createRandomArray() {
      // if in local storage there isn't cardsNumber stored 
      if (localStorage.getItem('cardsNumber') === null) {
        // set in local Storage the cards Number
        localStorage.setItem('cardsNumber', this.cardsNumber);
        // for loop to create, from the crocodilesArray, the gamingCardsArray with the right number of cards related with the choosen level 
        for (let i = 0; i < this.cardsNumber; i++) {
          this.gamingCardsArray.push(this.crocodilesArray[i]);
        }
        // get random the elements in the array
        this.gamingCardsArray = this.gamingCardsArray.sort(() => 0.5 - Math.random());
      // if in local storage there is cardsNumber stored (this means that we want to change level)
      } else {
        // clear the localStorage from the old cardsNumber value
        localStorage.clear();
        // add the new cardsNumber Value in the localStorage
        localStorage.setItem('cardsNumber', this.cardsNumber);
        // reload the page (the new cardsNumber in localStorage will be used beforeMount)
        location.reload();
      }
    },
  }
}
</script>

<style scoped lang="scss">
.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: #F2F5C8;
}
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
.choiceBox_select {
  margin-right: 4rem;
  padding: 0.5rem;
  color: black;
  font-size: larger;
  font-weight: bolder;
  background-color: #C1DEAE;
  border: none;
  box-shadow: 5px 5px 2px #219F94;
  outline: none;
  cursor: pointer;
}
.choiceBox_button {
  padding: 0.5rem 1.5rem;
  color: black;
  font-size: large;
  font-weight: bold;
  background-color: #C1DEAE;
  border: none;
  box-shadow: 5px 5px 2px #219F94;
  cursor: pointer;
}
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
  cursor: pointer;
}
.container_bottom .card:hover {
  transform: scale(1.1);
}
.card_img {
  width: 100%;
  height: 100%;
  display: none;
}
</style>
