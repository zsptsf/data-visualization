<template>
    <div>
        <Chart :cdata="cdata" chartID="csj"/>
    </div>
</template>

<script>
    import Chart from './chart.vue';
    export default {
        data () {
            return {
                cdata: {
                    populationData: [
                        {value: 1.57, name: '长三角城市群'},
                        {value: 13.51, name:'全国其他地区'},
                    ],
                    areaData: [
                        {value: 21.17, name: '长三角城市群'},
                        {value: 915.22, name:'全国其他地区'},
                    ],
                    GDPData: [
                        {value: 20.51, name: '长三角城市群'},
                        {value: 89.78, name:'全国其他地区'},
                    ],
                    seriesData:  [
                        {value: 38701, name: '上海'},
                        {value: 20171, name: '苏州'},
                        {value: 16106, name: '杭州'},
                        {value: 14818, name: '南京'},
                        {value: 12409, name: '宁波'},
                        {value: 12370, name: '无锡'},
                        {value: 10046, name: '合肥'},
                        {value: 10036, name: '南通'},
                        {value: 7805, name: '常州'},
                        {value: 6048, name: '扬州'},
                        {value: 6001, name: '绍兴'},
                        {value: 5953, name: '盐城'},
                        {value: 5510, name: '嘉兴'},
                        {value: 5313, name: '泰州'},
                        {value: 5263, name: '台州'},
                        {value: 4704, name: '金华'},
                        {value: 4220, name: '镇江'},
                        {value: 3753, name: '芜湖'},
                        {value: 3201, name: '湖州'},
                        {value: 3032, name: '滁州'},
                        {value: 2468, name: '安庆'},
                        {value: 2187, name: '马鞍山'},
                        {value: 1608, name: '宣城'},
                        {value: 1512, name: '舟山'},
                        {value: 1004, name: '铜陵'},
                        {value: 869, name: '池州'}
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