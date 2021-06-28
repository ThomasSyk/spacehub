<template>
    <div>
        <v-app-bar
            color="dark"
            dark
            dense  
        >
            <v-img :src="require('../assets/logo.png')" max-height="50" max-width="50"  />
            <v-toolbar-title>SPACEHUB</v-toolbar-title>
                <v-btn 
                 text
                 to="/"
                >
                    Home
                </v-btn>
                <v-menu
                 open-on-hover
                 offset-y
                >
                <template v-slot:activator="{ on }">
                    <v-btn
                    text
                    v-on="on"
                    to="/gallery"
                    @click="onClickButton(pickedGallery[0])"
                    >
                    Galerie
                    </v-btn>
                </template>

                <v-list >
                    <v-list-item>
                        <v-btn text to="/gallery" @click="onClickButton(pickedGallery[1])"> Earth</v-btn>
                    </v-list-item>
                    <v-list-item>
                         <v-btn text to="/gallery" @click="onClickButton(pickedGallery[2])"> Mars</v-btn>
                    </v-list-item>
                    <v-list-item>
                        <v-btn text to="/gallery" @click="onClickButton(pickedGallery[3])"> Sun</v-btn>
                    </v-list-item>
                    <v-list-item>
                        <v-btn text to="/gallery" @click="onClickButton(pickedGallery[4])"> Jupiter</v-btn>
                    </v-list-item>
                    <v-list-item>
                        <v-btn text to="/gallery" @click="onClickButton(pickedGallery[5])"> Saturn</v-btn>
                    </v-list-item>
                </v-list>
                </v-menu>
                <v-menu
                open-on-hover
                offset-y
                >
                <template v-slot:activator="{ on }">
                    <v-btn
                    text
                    v-on="on"
                    to="/roverGallery"
                    @click="onClickButton(pickedRover[0])"
                    >
                    Mars Rover
                    </v-btn>
                </template>
                <v-list>
                    <v-list-item>
                        <v-btn text to="/roverGallery" @click="onClickButton(pickedRover[0])"> Curiosity</v-btn>
                    </v-list-item>
                    <v-list-item>
                         <v-btn text to="/roverGallery" @click="onClickButton(pickedRover[1])"> Opportunity</v-btn>
                    </v-list-item>
                    <v-list-item>
                        <v-btn text to="/roverGallery" @click="onClickButton(pickedRover[2])"> Spirit</v-btn>
                    </v-list-item>
                </v-list>
                </v-menu>
        </v-app-bar>
    </div>
</template>

<script>
export default {
  name: 'Navbar',
  data (){
      return {
          pickedGallery: ['', 'earth', 'mars', 'sun', 'jupiter', 'saturn'],
          pickedRover: ['curiosity', 'opportunity', 'spirit']

      }
  },
  methods: {
    onClickButton (data) {
      this.$emit('clicked', data)
    }
  }
}
</script>

<style>

</style>