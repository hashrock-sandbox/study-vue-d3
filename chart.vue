<style>

  .node {
    stroke-width: 1.5px;
  }
  svg{
    border: solid 1px black;
    background: #99FF5F;
  }

</style>

<template>
  <p></p>
  <svg width="600px" height="600px"></svg>
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
  
  var node;
  var width = 600;
  var height = 600;

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
      function tick() {
        node.attr("x", function(d) { return d.x; })
            .attr("y", function(d) { return d.y; });
      }
      
      var nodes = d3.range(30).map(function(i) {
        return {index: i};
      });
      var force = d3.layout.force()
          .nodes(nodes)
          .size([width, height])
          .charge(-1000)
          .on("tick", tick)
          .start();
          
      var svg = d3.select("svg");
      
      node = svg.selectAll(".node")
        .data(nodes)
        .enter().append("image")
        .attr("class", "node")
        .attr("xlink:href", "cloud-hi.png")
        .attr("x", function(d){return d.x})
        .attr("y", function(d){return d.y})
        .attr("height", "200px")
        .attr("width", "200px")
        //.attr("cx", function(d){return d.x})
        //.attr("cy", function(d){return d.y})
        //.attr("r", 16)
        .call(force.drag);
        
        
    }
  }
</script>