<script>
import * as d3 from 'd3';
import { ref } from 'vue'
import { useIsSlideActive } from '@slidev/client'

export default {
  data() {
    return { count: 0, rowCnt: 100, colCnt: 100, cellCnt: 10_000, stepCnt: 3, gridID: "" };
  },
  props: {
    gridID: String,
    gridActive: Boolean,
    gridSteps: Number,
  },
  setup(props) {
    const count = ref(0);
    const redraw = ref(0);
    const sfc32 = function (a, b, c, d) {
      return function () {
        a |= 0; b |= 0; c |= 0; d |= 0;
        let t = (a + b | 0) + d | 0;
        d = d + 1 | 0;
        a = b ^ b >>> 9;
        b = c + (c << 3) | 0;
        c = (c << 21 | c >>> 11);
        c = c + t | 0;
        return (t >>> 0) / 4294967296;
      }
    };
    const gridID = ref(props.gridID);
    const active = ref(props.gridActive);
    const stepCnt = ref(props.gridSteps);
    const isActive = useIsSlideActive()

    return { count, redraw, sfc32, gridID, active, stepCnt, isActive }
  },
  mounted() {
    this.drawGrid();
  },
  unmounted() {
    this.clearGrid();
  },
  watch: {
    count: {
      handler(nV) {
        // console.log("new count " + nV + " for grid " + this.gridID + " with state " + this.isActive);
        if (!this.isActive) {
          return
        }
        setTimeout(this.stepGrid, 1);
      },
    },
    isActive: {
      handler(nV) {
        if (nV) {
          console.log("active is now true for grid " + this.gridID);
          this.clearGrid();
          this.stepGrid();
        } else {
          console.log("active is now false for grid " + this.gridID);
          this.count = 0;
          this.clearGrid();
        }
      },
    },

  },
  methods: {
    clearGrid() {
      this.drawGrid();
      this.count = 0;
    },
    resetGrid() {
      this.count = 0;
    },
    emptyGrid() {
      var data = new Array();
      var xpos = 1;
      var ypos = 1;
      var width = 5;
      var height = 5;
      var cellIdx = 0;

      var getRand = this.sfc32(1, 2, 3, 4);

      for (var row = 0; row < this.rowCnt; row++) {
        data.push(new Array());
        for (var col = 0; col < this.colCnt; col++) {
          var fco = "#000";
          data[row].push({
            x: xpos,
            y: ypos,
            width: width,
            height: height,
            fill: fco,
            id: "wd-" + this.gridID + "-" + cellIdx,
            rnd: getRand(),
          })
          xpos += width;
          cellIdx++;
        }
        xpos = 1;
        ypos += height;
      }
      return data;
    },
    getRandomColor(v) {
      return `hsla(${Math.random() * 360}, 100%, 50%, 0.80)`
    },
    updateGrid() {
      if (!this.isActive) {
        return
      }
      for (var c = this.count; c <= (this.count + this.stepCnt); c++) {
        if (c > this.cellCnt) {
          break;
        }

        var cell = d3.select("#wd-" + this.gridID + "-" + c);
        if (cell.empty()) {
          break;
        }

        var v = Number(cell.attr("rnd"));

        console.log("v for count " + this.count + " is " + v);
        var fco = "#000";
        if ((c > 1000) && (c < 1200)) {
          if (v > 0.65) {
            fco = "green";
          } else if (v > 0.50) {
            fco = "#444";
          }
        } else if (c >= 4500 && c < 5000) {
          // 
        } else if (c >= 5200 && c < 5600) {
          fco = "darkred";
        } else if (c >= 7500 && c < 7700) {
          // 
        } else if (c >= 9500 && c < 9900) {
          // 
        } else if (v > 0.999) {
          fco = "white";
        } else if (v > 0.99) {
          fco = "darkred";
        } else if (v > 0.989) {
          fco = "green";
        } else if (v > 0.96) {
          fco = "blue";
        } else if (v > 0.95) {
          fco = "orange";
        } else if (v > 0.70) {
          fco = "#444";
        }
        d3.select("#wd-" + this.gridID + "-" + c).style("fill", fco);
        for (var x = 1; x < (this.stepCnt * v * 10); x++) {
          if (x % 23 == 0 || x % 7 == 0) {
            d3.select("#wd-" + this.gridID + "-" + (c + x)).style("fill", this.getRandomColor(v));
          } else {
            d3.select("#wd-" + this.gridID + "-" + (c + x)).style("fill", "none");
          }
        }
      }
      this.count += this.stepCnt
    },
    drawGrid() {
      var thisGrid = '#' + this.gridID;
      var gridData = this.emptyGrid();
      d3.select(thisGrid).selectAll("*").remove();

      var grid = d3.select("#" + this.gridID)
        .append("svg")
        .attr("height", this.rowCnt * 6)
        .attr("width", this.colCnt * 6);

      var row = grid.selectAll(".row")
        .data(gridData)
        .enter().append("g")
        .attr("class", "row");

      var column = row.selectAll(".square")
        .data(function (d) { return d; })
        .enter().append("rect")
        .attr("class", "square")
        .attr("id", function (d) { return d.id; })
        .attr("rnd", function (d) { return d.rnd; })
        .attr("x", function (d) { return d.x; })
        .attr("y", function (d) { return d.y; })
        .attr("width", function (d) { return d.width; })
        .attr("height", function (d) { return d.height; })
        .style("stroke", "#222")
        .style("fill", function (d) { return d.fill; })
    },
    stepGrid() {
      var cellCnt = this.rowCnt * this.colCnt;
      if (this.count > cellCnt) {
        this.resetGrid();
      }
      this.updateGrid();
    },
  }
};
</script>

<template>
  <div :id="gridID" class="wardialGrid" @click="clearGrid()"></div>
</template>

<style scoped>
.wardialGrid {
  position: absolute;
  top: 2%;
  left: 48%;
  width: 45%;
  height: 45%;
}
</style>