<template>
    <div id="pageBox">
        <v-pagination
          v-model="page"
          :length="pageMax"
          total-visible="10"
          @input="onClickPageButton(page)"
        ></v-pagination>
    </div>
</template>

<script>

  export default {
      props: ['pageMax'],
    data () {
      return {
          page: 1
      }
    },
    methods: {
      onClickPageButton (data) {
        this.$emit('clicked', data)
        console.log("Page")
    }
  }
  }
</script>

<style scoped>
#pageBox{
    padding: 10px;
}
</style>