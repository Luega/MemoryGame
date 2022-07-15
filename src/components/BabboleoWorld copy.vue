<template>
  <!-- `container -->
  <div class="container">
    <!-- top -->
    <div>
      <!-- title and button -->
      <div class="topContainer">
        <h1>CIAO LELE INIZIA A GIOCARE</h1>
        <button>GIOCA</button>
      </div>
    </div>    
    <!-- bottom -->
    <div>
      <!-- playgorund -->
      <div class="playground">
        <!-- run a v-for on the crocodilesArray array to create cards  -->
        <!-- added the click event to change the display mode of the card's img -->
        <div :id="`a-${key}`" class="card" v-for="(croc, key) in crocodilesArray" :key="key" @click="selectCard(croc, key)">
        <!-- added the id to select the img in the function 'selectCard' -->
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
      // array for the imgs comparison
      comparisonArray: [],
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
      // depending on truthfulness of the selected 
      if (croc.selected == false) {
        // change selected value of the card 
        croc.selected = true; 
        // change the display mode of the card's img
        document.getElementById(`ab-${key}`).style.display = "inline-block";
        // push the obj in the comparison array
        this.comparisonArray.push(croc);
        // after the second card selection
        if (this.comparisonArray.length == 2) {
          // if the img of obj are the same
          if (this.comparisonArray[0].img == this.comparisonArray[1].img) {
            // push the first obj of comparisonArray in to endingArray
            this.endingArray.push(this.comparisonArray[0]);
            // remove the objts from comparisonArray
            this.comparisonArray.splice(0, 2);
            alert("hai 0 elementi nell'array");
          }
        }
      } else {
        croc.selected = false;
        document.getElementById(`ab-${key}`).style.display = "none";
      }
      // 1- creo due array vuoti (uno per il confronto e uno per la fine del gioco)
      // 2- la lunghezza dell'array é minore di 2
      // 3- vai avanti
      // 4- la lunghezza dell'array é maggiore o uguale a 2
      // 5- se img sono uguali allora allert, aggiungo card all'array e poi la card cambia display in none 
      // 6- se img sono diverse le img display none e l´array viene svuotato.
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
.playground {
  padding: 2rem;
  border: 2px solid black;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.playground .card {
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
