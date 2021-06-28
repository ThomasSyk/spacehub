<!--TO_DO Bilder Clickbar verdeutlichen  -->
<template>
  <div>
    <v-row>
    <v-col
      v-for="result in imageArray"
      :key="result.items"
      class="d-flex child-flex"
      cols="2"
    >
      <v-hover  v-slot="{hover}">
        <v-card
        :elevation="hover ? 16 : 2"
        :class="{ 'on-hover': hover }"
        @click="overlayActivate = !overlayActivate; imgLink = result.links[0].href; description = result.data[0].description"
        >
            <v-img 
            :src="result.links[0].href"
            aspect-ratio="1"
            class="grey lighten-2"
            >
            </v-img>
            <v-overlay
              v-if="hover"
              absolute
              color="#EEEEEE"
            >
              <v-btn>
                Klick for Info
              </v-btn>
            </v-overlay>  
        </v-card>
      </v-hover>
    </v-col>
    </v-row>
    
    <PictureOverlay 
      :imageSrc="imgLink" 
      :description="description" 
      @clicked="onClickChild"
      v-if="overlayActivate"
    />
  </div>
</template>

<script>
import PictureOverlay from './PictureOverlay';
export default {
    components: {
       PictureOverlay
    },
    props: ['imageArray'],
    data (){
    return{
      overlayActivate: false,
      imgLink: '', //Speichern der aktuellen url fuer das Bild was im overlay angezeigt wird
      description: ''
    }
  },
  methods: {
    onClickChild (value) {
      this.overlayActivate = value; // someValue
    }
  }
}
</script>

<style scoped>
</style>