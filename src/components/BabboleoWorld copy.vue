<template>
  <!-- CONTAINER -->
  <div class="container">
    <!-- TOP -->
    <div>
      <!-- TITLE -->
      <div class="topContainer">
        <h1>CIAO LELE INIZIA A GIOCARE</h1>
        <!-- SELECTION OF THE LEVEL -->
        <button>GIOCA</button>
      </div>
    </div>    
    <!-- BOTTOM -->
    <div>
      <!-- PLAYGROUND -->
      <div id="playground">
        <!-- CARDS -->
        <!-- run a v-for on the crocodilesArray to create cards and added the click event -->
        <div class="card" v-for="(croc, key) in crocodilesArray" :key="key" @click="selectCard(croc, key)">
          <img :id="`ab-${key}`" :src="require(`@/assets/img/${croc.img}`)" alt="Croc">
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
      cardsNumber: 16,
      // array for the imgs comparison
      comparisonArray: [],
      // array of img ids to change the display mode of the imgs if the imgs selected are not the same
      idArray: [],
      // array for the ending of the game
      endingArray: [],
      // array for the cards
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
          img: "cartoon-crocodile-vector-21277180.jpg",
          selected: false,
        },
        {
          img: "cartoon-crocodile-vector-21277180.jpg",
          selected: false,
        },
        {
          img: "cartoon-crocodile-vector-21277180.jpg",
          selected: false,
        },
        {
          img: "cartoon-crocodile-vector-21277180.jpg",
          selected: false,
        },
        {
          img: "cartoon-crocodile-vector-21277180.jpg",
          selected: false,
        },
        {
          img: "cartoon-crocodile-vector-21277180.jpg",
          selected: false,
        },
        {
          img: "cartoon-crocodile-vector-21277180.jpg",
          selected: false,
        },
        {
          img: "cartoon-crocodile-vector-21277180.jpg",
          selected: false,
        },
        {
          img: "cartoon-crocodile-vector-21277180.jpg",
          selected: false,
        },
        {
          img: "cartoon-crocodile-vector-21277180.jpg",
          selected: false,
        },
        {
          img: "cartoon-crocodile-vector-21277180.jpg",
          selected: false,
        },
        {
          img: "cartoon-crocodile-vector-21277180.jpg",
          selected: false,
        }
      ]
    }
  },
  methods: {
    selectCard(croc, key) {
      // if the selected value of the card is false
      if (croc.selected == false) {
        // change selected value of the card 
        croc.selected = true; 
        // change the display mode of the card's img
        document.getElementById(`ab-${key}`).style.display = "inline-block";
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
              alert('hai vinto!')
            }
            // if the img of objs are not the same
          } else if (this.comparisonArray[0].img !== this.comparisonArray[1].img) { 
            // change the display imgs of both selected cards to none
            document.getElementById(this.idArray[0]).style.display = "none";
            document.getElementById(this.idArray[1]).style.display = "none";
            // remove the ids from idArray
            this.idArray.splice(0, 2);
            // change the card selected value to false
            this.crocodilesArray.forEach(obj => {
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
  }
}
</script>

<style scoped lang="scss">
.container {
  width: 100%;
  height: 100vh;
  padding: 2rem;
  text-align: center;
}
.topContainer {
  padding: 2rem;
  display: flex;
  justify-content: space-between;
}
#playground {
  padding: 2rem;
  border: 2px solid black;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
#playground .card {
  width: 100px;
  height: 100px;
  margin: 10px;
  background-color: yellow;
  border: 1px solid black;
  flex-basis: calc((100% / 5) - 20px);
  display: flex;
  justify-content: center;
  align-items: center;
}
.card img {
  width: 100%;
  height: 100%;
  display: none;
}
</style>
