<template>
    <div>
      <v-row>
        <v-col
            v-for="result in RoverImageArray"
            :key="result.item"
            class="d-flex child-flex"
            cols="3"
        >
            <v-hover  v-slot="{hover}">
                <v-card
                :elevation="hover ? 16 : 2"
                :class="{ 'on-hover': hover }"
                @click="overlayActivate = !overlayActivate; imgLink = result.img_src; description = result.id"
                >
                    <v-overlay
                        v-if="hover"
                        absolute
                        color="#EEEEEE"
                    >
                        <v-btn>
                            Klick for Info
                        </v-btn>
                    </v-overlay>  
                    <v-img 
                    :src="result.img_src.replace('http', 'https')"
                    aspect-ratio="1"
                    class="grey lighten-2"
                    >
                    </v-img>
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
    props: ['RoverImageArray'],
    components: {
        PictureOverlay
    },
    data (){
        return{
            overlayActivate: false,
            imgLink: '', //Speichern der aktuellen url fuer das Bild was im overlay angezeigt wird
            description: ''
    }
  },
   methods: {
    onClickChild (value) {
      console.log(value)
      this.overlayActivate = value; // someValue
      console.log(this.overlayActivate)
    }
  }
}
</script>