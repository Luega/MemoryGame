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
        <!-- run a v-for on the crocodiles array to create cards  -->
        <!-- added the click event to change the display mode of the card's img -->
        <div class="card" v-for="(croc, key) in crocodiles" :key="key" @click="selectCard(croc, key)">
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
      crocodiles: [
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
      // depending on truthfulness of the croc.selected we change it with its opposite and after we change the display mode of the card's img thanks to unique id
      if (croc.selected == false) {
        croc.selected = true;
        document.getElementById(`ab-${key}`).style.display = "inline-block";
      } else {
        croc.selected = false;
        document.getElementById(`ab-${key}`).style.display = "none";
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
