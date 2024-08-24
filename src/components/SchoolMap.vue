<template>
    <div ref="chart" style="width: 100%; height: 800px;"></div>
</template>

<script>
import * as echarts from 'echarts';
import china from '@/assets/json/china.json'
import axios from 'axios';

function getUniversityCount(provinceName) {
    return axios.get(`${this.$config.serverUrl}/api/universities/${provinceName}`)
        .then(response => response.data.count)
        .catch(() => 0);
}

export default {
    name: "SchoolMap",
    mounted() {
        this.initCharts();
    },
    methods: {
        async initCharts() {
            const chart = echarts.init(this.$refs.chart);
            echarts.registerMap('china', china);
            const option = {
                tooltip: {
                    trigger: 'item',
                    formatter: async function(params) {
                        const provinceName = params.name;
                        const universityCount = await getUniversityCount(provinceName);
                        return `${provinceName}: ${universityCount}`
                    }
                },
                series: [{
                    type: 'map',
                    map: 'china',
                    label: {
                        show: false
                    },
                    itemStyle: {
                        emphasis: {
                            areaColor: '#a1c4fd'
                        }
                    }
                }]
            }
            chart.setOption(option)
        }
    }
}

</script>
