<template>
    <div>
        <h1>Picture Gallery </h1>
        <div id="imageCollectionBox">
          <div>
            <Search @clicked="onSearch"/>
          </div>
          <h2> Selected: {{selection}}</h2>
          <PictureCollection :imageArray="results"/>
          <Pagination v-if="!searchSet" :pageMax="pagecount" @clicked="onClickPage"/>  
          <p v-if="results.length == 0">No Pictures found</p>
        </div>
    </div>
</template>

<script>
import PictureCollection from '../components/PictureCollection'
import Pagination from '../components/Pagination'
import Search from '../components/Search'
import axios from 'axios'

export default {
  components: {
    PictureCollection,
    Pagination,
    Search
  },
  //selection beinhaltet die standard auswahlmoeglichkeiten der Galerie 
  props: ["selection"],
  data (){
    return{
      results: '',
      page: 1,
      pagecount: 1,
      search: '',
      searchSet: false
    }
  },
  //watch function um prop "selection" auf aenderungen zu Ueberwachen. Wird eine aenderung festgestellt wird ein neuer Api-Call ausgefuehrt.
  watch: {
    selection: {
      immediate: true, //wird verwendet um von beginn an auf prop veraenderungen zu reagieren. 
      deep: true, // wird verwendet wenn ein Array Ueberwacht werden soll.
      // handler-methode um auf aenderung der prop selction zu reagieren 
      handler(){
        this.searchSet = false;
        axios.get('https://images-api.nasa.gov/search?q=' + this.selection + '&page=1&media_type=image').then ( response => {
          console.log(response.data.collection.items); // console.log nur zu testszwecken um die api response zu Pruefen
          this.results = response.data.collection.items;
          this.pagecount = parseInt(response.data.collection.metadata.total_hits / 100);
          //If-Abfrage falls pagecount groesser als 100, wird pagecount auf 100 gestzt da die api nicht mehr als Page 100 zulaesst
          if(this.pagecount > 100){   
            this.pagecount = 100;
          }
        });
      } 
    }
  },
  methods: {
    onClickPage (value) {
      this.searchSet = false;
      this.page = value; 
      axios.get('https://images-api.nasa.gov/search?q=' + this.selection + '&page=' + this.page + '&media_type=image').then ( response => {
          console.log(response.data.collection.items); // console.log nur zu testszwecken um die api response zu Pruefen
          this.results = response.data.collection.items;
        });
    },
    onSearch (data) {
      this.search = data;
      axios.get('https://images-api.nasa.gov/search?q=' + this.search + '&media_type=image').then ( response => {
        console.log(response.data.collection.items); // console.log nur zu testszwecken um die api response zu Pruefen
        this.results = response.data.collection.items;
        console.log("Total Entrys: " + response.data.collection.metadata.total_hits); //testszwecken anzeige der Entrys in der Console
        this.searchSet = true;
          
      });
    }
  }
}

</script>

<style scoped>
#imageCollectionBox{
  margin: auto;
  max-width: 60%;
}

h1{
  text-align: center;
  padding: 40px;
}
h2{
  padding: 20px;
}
</style>