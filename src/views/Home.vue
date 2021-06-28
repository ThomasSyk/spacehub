<template>
<!-- v-carousel Funktion einfügen -->
  <div class="mainHome">
    <div class="apodBox">
      <h1>Astronomic Pictures of the recent Days</h1>
      <PictureCarousel :resultArray="results"/>
    </div>
  </div>
</template>

<script>
import PictureCarousel from '../components/PictureCarousel';
import axios from 'axios'

export default{
  components: {
    PictureCarousel
  },
  data () {
    return {
      results: ''
    }
  },
  //mit axios daten für picture of the day ranholen
  mounted(){
    axios.get('https://api.nasa.gov/planetary/apod?api_key=FAtndhzJANYxmE62dLaOSEpyyEyd2lB3E2b2nrdh&start_date=2021-06-01').then ( response => {
    console.log(response.data);
    this.results = response.data;
    });
  }
}

</script>

<style scoped>
h1{
  text-align: center;
  padding: 40px;
}

.apodBox{
  max-width: 70%;
  margin: auto;
  color: #060020;
  
}

</style>
