<template>
    <div ref="plotATGCSV" id="plotATGCSV"></div>
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
                this.dataRows = await d3.csv(this.filePath);
                this.drawPlot();
            } catch (error) {
                console.error('Error loading plotly data:', error);
            }
        },
        drawPlot() {
            if (!Plotly) {
                return;
            }

            var rows = this.dataRows;
            function unpackNum(rows, key) {
                return rows.map(function (row) { return Number(row[key]); });
            }
            function unpackStr(rows, key) {
                return rows.map(function (row) { return row[key]; });
            }

            var trace1 = {
                type: "scatter",
                mode: "lines",
                name: 'CouchShop',
                x: unpackStr(rows, 'Date'),
                y: unpackNum(rows, 'CouchShop'),
                line: { color: 'lightyellow' }
            }

            var trace2 = {
                type: "scatter",
                mode: "lines",
                name: 'FlowerShop',
                x: unpackStr(rows, 'Date'),
                y: unpackNum(rows, 'FlowerShop'),
                line: { color: 'lightgreen' }
            }


            var trace3 = {
                type: "scatter",
                mode: "lines",
                name: 'JewelryShop',
                x: unpackStr(rows, 'Date'),
                y: unpackNum(rows, 'JewelryShop'),
                line: { color: 'lightblue' }
            }

            var data = [trace1, trace2, trace3];
            var layout = {
                paper_bgcolor: 'rgba(0,0,0,0)',
                plot_bgcolor: 'rgba(0,0,0,0)',
                color: 'white',
                showlegend: true,
                xaxis: {
                    autorange: true,
                    range: ['2015-03-01', '2017-04-29'],
                    color: 'white',
                    showgrid: false,
                    font: {
                        color: 'white'
                    }
                },
                yaxis: {
                    autorange: true,
                    type: 'log',
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
            Plotly.newPlot(this.$refs.plotATGCSV, data, layout, { displayModeBar: false, responsive: true });
        }
    }
}
</script>


<style>
#plotATGCSV {
    padding: 0;
    margin: 0;
    margin-top: -4rem;
}
</style>