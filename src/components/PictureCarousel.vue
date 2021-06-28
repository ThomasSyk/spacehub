<template>
    <div>
        <v-carousel 
        hide-delimiters
        height="1000"
        >
            <v-carousel-item
              v-for="(item,i) in resultArray"
              :key="i"
              height="10"
            >
                <v-img :src="item.hdurl" height="80%" ></v-img>
                <h2>{{item.title}} {{item.date}}</h2>
                <span>{{item.explanation}}</span>
            </v-carousel-item>
        </v-carousel>
    </div>
</template>

<script>
export default {
    props: ['resultArray']
    
}
</script>