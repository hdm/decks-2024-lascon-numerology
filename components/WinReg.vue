<template>
    <div ref="plotWinReg" id="plotWinReg"></div>
</template>

<script>

import * as d3 from 'd3';
import Plotly from 'plotly.js-dist-min'

export default {
    props: {
        filePath: String,
        graphWidth: Number,
        graphHeight: Number,
        xTitleFontSize: Number,
        yTitleFontSize: Number,
        tickFontSize: Number,
        annotationFontSizeScale: Number,
    },
    data() {
        return {

        };
    },

    mounted() {
        this.createPlot();
    },
    methods: {
        loadPlotlyScript() {
            return new Promise((resolve, reject) => {
                if (window.Plotly) {
                    resolve();
                }
            });
        },
        async createPlot() {
            if (!this.filePath) return;

            try {
                this.dataSet = await d3.json(this.filePath);
                this.drawPlot();
            } catch (error) {
                console.error('Error loading plotly data:', error);
            }
        },
        drawPlot() {
            if (!Plotly) {
                return;
            }

            var data = [
                {
                    x: [],
                    y: [],
                    type: 'bar'
                }
            ];

            var sortedSet = [];
            for (var i in this.dataSet.vendors) {
                sortedSet.push({ vendor: i, count: this.dataSet.vendors[i] })
            }
            sortedSet = sortedSet.sort(function (a, b) {
                return b.count - a.count;
            })

            for (var i in sortedSet) {
                var v = sortedSet[i];
                data[0].x.push(v.vendor);
                data[0].y.push(v.count);
                if (i > 3) {
                    break;
                }
            }

            var layout = {
                paper_bgcolor: 'rgba(0,0,0,0)',
                plot_bgcolor: 'rgba(0,0,0,0)',
                color: 'white',
                showlegend: false,
                xaxis: {
                    autorange: true,
                    //range: ['2015-03-01', '2017-04-29'],
                    color: 'white',
                    showgrid: false,
                    font: {
                        color: 'white'
                    }
                },
                yaxis: {
                    autorange: true,
                    //  type: 'log',
                    color: 'white',
                    showgrid: false,
                    font: {
                        color: 'white'
                    }
                },

                legend: {
                    font: {
                        color: 'white',
                    }
                }
            };
            Plotly.newPlot(this.$refs.plotWinReg, data, layout, { displayModeBar: false, responsive: true });
        }
    }
}
</script>


<style>
#plotWinReg {
    padding: 0;
    margin: 0;
    margin-top: -4rem;
}
</style>