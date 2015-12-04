<style>
</style>

<template>
  <input type="text" v-model="text">
  <chart :input="text"></chart>
</template>

<script>
  var chart;
  module.exports = {
    data: function () {
      return {
        msg: 'Hello world!',
        text: "hello"
      }
    },
    components: {
      chart : require("./chart.vue")
    }
  }
</script>