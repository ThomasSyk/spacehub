<template>
  <v-app>
    <v-main>
      <Navbar @clicked="onClickChild"/>
      <router-view 
        :selection="routingInfo"
      />
    </v-main>
  </v-app>
</template>

<script>
import Navbar from './components/NavBar';

export default {
  name: 'app',
  components: {
    Navbar
  },
  methods: {
    onClickChild (value) {
      console.log(value)
      this.routingInfo = value; 
      console.log(this.routingInfo)
    },
  },
  data (){
    return {
        routingInfo: '',
    }
  }
}

</script>


