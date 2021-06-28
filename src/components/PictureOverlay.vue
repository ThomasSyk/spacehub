<template>
    <v-overlay
     color="#E0E0E0"
     opacity="0.9"
    >
        <div>
            <v-btn color="error" @click="onClick(false)">Close</v-btn>
            <v-card @click="onClick(false)" max-width="1000">
                
                <v-img :src="imageSrc"></v-img>
                <p>{{description}}</p>
            </v-card>
        </div>
    </v-overlay>
</template>

<script>
export default {
    props: ['imageSrc', 'description'],
    data (){
        return {
            
        }
    },
    methods: {
        onClick (data) {
            this.$emit('clicked', data)
    }
  }
}
    
</script>

<style scoped>

</style>