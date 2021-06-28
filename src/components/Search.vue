<template>
    <div id="search">
        <v-row>
            <v-col
              class="d-flex child-flex"
              cols="auto"
              
            >
            <div id="searchField">
                <v-text-field
                v-model="search"
                append-icon="mdi-magnify"
                label="Search"
                single-line
                hide-details
                v-on:keyup.enter="getSearch(search)"
                ></v-text-field>
            </div>
                <v-btn large @click="getSearch(search)">Search</v-btn>
            </v-col>
        </v-row>
        
    </div>
</template>

<script>
export default {
    data(){
        return {
            search: ''
        }
    },
    methods: {
      getSearch (data) {
        this.$emit('clicked', data)
        console.log("Search " + data)
      }
    }
}
</script>

<style scoped>

#search {
    margin: auto;
    max-width: 500px;
}
</style>