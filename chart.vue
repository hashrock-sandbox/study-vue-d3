<style>

</style>

<template>
  <p></p>
</template>

<script>
  var d3 = require("d3");
  
  var Chart = function(el){
    this.el = el;
    this.$el = d3.select(el);
  }
  
  Chart.prototype.update = function(data){
    this.$el.text(data);
  }
  var chart;

  module.exports = {
    props: ["input"],
    data: function () {
      return {}
    },
    watch: {
      "input" : function(val){
        chart.update(val);
      }
    },
    ready: function(){
      chart = new Chart("p");
      chart.update(this.input);
    }
  }
</script>