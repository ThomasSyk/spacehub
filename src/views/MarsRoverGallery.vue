<template>
    <div>
        <h1>Mars Rover Galerie</h1>
        <div id="imageCollectionBox">
          <h2>Selected Rover: {{selection}}</h2>
          <p v-if="results.length">{{results[0].earth_date}}</p>
          <p v-else id="noPic"> No Pictures for this Date</p>
          <PictureCollectionMarsRover :RoverImageArray="results" />
          <Pagination :pageMax="pagecount" @clicked="onClickPage"/>

        </div>
    </div>
</template>

<script>
import PictureCollectionMarsRover from '../components/PictureCollectionMarsRover';
import Pagination from '../components/Pagination'
import axios from 'axios';
//Searchbar einbauen 
export default {
  props: ["selection"],
  components: {
    PictureCollectionMarsRover,
    Pagination
  },
  data (){
    return{
      results: '',
      sol: 1,
      pagecount: 100,
      paginationRedraw: false
    }
  },
  //watch function um prop "selection" auf aenderungen zu Ueberwachen. Wird eine aenderung festgestellt wird ein neuer Api-Call ausgefuehrt.
  watch: {
    selection: {
      immediate: true, //wird verwendet um von beginn an auf prop veraenderungen zu reagieren. 
      deep: true, // wird verwendet wenn ein Array Ueberwacht werden soll.
      // handler-methode um auf aenderung der prop selction zu reagieren 
      handler(){
        //If-Abfrage ob Daten fuer comp MarsRoverGalerie Gedacht sind 
        if(this.selection == 'curiosity' || this.selection == 'opportunity' || this.selection == 'spirit'){
          alert('Rover')
          console.log(this.selection)
          axios.get('https://api.nasa.gov/mars-photos/api/v1/rovers/'+ this.selection +'/photos?sol=' + this.sol + '&page=1&api_key=FAtndhzJANYxmE62dLaOSEpyyEyd2lB3E2b2nrdh').then ( response => {
            console.log(response.data.photos); // console.log nur zu testszwecken um die api response zu Pruefen
            this.results = response.data.photos;
            this.paginationRedraw = true;
          });
        }
      }
    }
  },
  methods: {
    onClickPage (value) {
      console.log(value)
      this.sol = value; 
      console.log(this.sol)
      axios.get('https://api.nasa.gov/mars-photos/api/v1/rovers/'+ this.selection +'/photos?sol=' + this.sol + '&page=1&api_key=FAtndhzJANYxmE62dLaOSEpyyEyd2lB3E2b2nrdh').then ( response => {
            console.log(response.data.photos); // console.log nur zu testszwecken um die api response zu Pruefen
            this.results = response.data.photos;
        });
    }
  }
}
</script>

<style scoped>
#noPic{
  font-weight: bold;
  color: red;
}

#imageCollectionBox{
  margin: auto;
  max-width: 70%;
}

h1 {
  text-align: center;
  padding: 40px;
}
</style>
