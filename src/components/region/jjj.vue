<template>
    <div>
        <Chart :cdata="cdata" chartID="jjj"/>
    </div>
</template>

<script>
    import Chart from './chart.vue';
    export default {
        data () {
            return {
                cdata: {
                    populationData: [
                        {value: 1.13, name: '京津冀城市群'},
                        {value: 13.95, name:'全国其他地区'},
                    ],
                    areaData: [
                        {value: 21.5, name: '京津冀城市群'},
                        {value: 914.89, name:'全国其他地区'},
                    ],
                    GDPData: [
                        {value: 8.64, name: '京津冀城市群'},
                        {value: 101.65, name:'全国其他地区'},
                    ],
                    seriesData:  [
                        {value: 36103, name: '北京'},
                        {value: 14084, name: '天津'},
                        {value: 7211, name: '唐山'},
                        {value: 5935, name: '石家庄'},
                        {value: 3700, name: '沧州'},
                        {value: 3637, name: '邯郸'},
                        {value: 3353, name: '保定'},
                        {value: 3301, name: '廊坊'},
                        {value: 2200, name: '邢台'},
                        {value: 1686, name: '秦皇岛'},
                        {value: 1600, name: '张家口'},
                        {value: 1560, name: '衡水'},
                        {value: 1550, name: '承德'}
                    ]
                }
            }
        },
        components: {
            Chart,
        },
        mounted () {
        },
        methods: {
        }
    }
</script>