<template>
    <div>
        <Chart :cdata="cdata" chartID="zsj"/>
    </div>
</template>

<script>
    import Chart from './chart.vue';
    export default {
        data () {
            return {
                cdata: {
                    populationData: [
                        {value: 0.64, name: '珠三角城市群'},
                        {value: 14.44, name:'全国其他地区'},
                    ],
                    areaData: [
                        {value: 5.5, name: '珠三角城市群'},
                        {value: 930.89, name:'全国其他地区'},
                    ],
                    GDPData: [
                        {value: 8.95, name: '珠三角城市群'},
                        {value: 101.34, name:'全国其他地区'},
                    ],
                    seriesData:  [
                        {value: 27670, name: '深圳'},
                        {value: 25019, name: '广州'},
                        {value: 10816, name: '佛山'},
                        {value: 9650, name: '东莞'},
                        {value: 4222, name: '惠州'},
                        {value: 3482, name: '珠海'},
                        {value: 3201, name: '江门'},
                        {value: 3152, name: '中山'},
                        {value: 2312, name: '肇庆'},
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