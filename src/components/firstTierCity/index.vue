<template>
    <div>
        <Echart
                id="firstTierCity"
                :options="options"
                height="3rem"
        ></Echart>
    </div>
</template>
<script>
    import Echart from '@/common/echart';
    export default {
        name: "index",
        data() {
            return {
                options: {
                    dataset: {
                        source: [
                            ['GDP总量', '城市'],
                            [36103, '北京'],
                            [38701, '上海'],
                            [25019, '广州'],
                            [27670, '深圳']
                        ]
                    },
                    grid: {
                        right:'20%'
                    },
                    xAxis: {
                        name: 'GDP总量',
                        splitLine: {
                            show: false
                        },
                        axisLine: {
                            show: true,
                            lineStyle: {
                                color: '#fff'
                            }
                        },
                    },
                    yAxis: {
                        type: 'category',
                        axisLine: {
                            show: true,
                            lineStyle: {
                                color: '#fff'
                            }
                        },
                    },
                    series: [
                        {
                            type: 'bar',
                            barWidth:10,
                            encode: {
                                x: 'GDP总量',
                                y: '城市'
                            },
                            label: {
                                position: 'right',
                                show: true,
                                color:'#fff'
                            },
                        }
                    ]
                },
            };
        },
        components: {
            Echart,
        },
        methods: {
        }
    }
</script>