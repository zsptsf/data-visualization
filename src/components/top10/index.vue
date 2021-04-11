<template>
    <div>
        <Echart
                id="top10"
                :options="options"
                height="5.6rem"
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
                    color:[
                        '#67a1e5','#50e3c2','#D0648A'
                    ],
                    grid: {
                        left: '18%',
                        bottom:'10%'
                    },
                    tooltip: {
                        trigger: 'axis',
                        axisPointer: {
                            type: 'cross'
                        }
                    },
                    xAxis: [
                        {
                            type: 'category',
                            axisTick: {
                                alignWithLabel: true,
                            },
                            axisLabel:{
                                textStyle:{
                                    color:'#fff'
                                }
                            },
                            data: ['上海', '北京', '深圳', '广州', '重庆', '苏州', '成都', '杭州', '武汉', '南京']
                        }
                    ],
                    yAxis: [
                        {
                            type: 'value',
                            name: 'GDP总量\n（亿元）',
                            min: 0,
                            max: 38000,
                            position: 'left',
                            axisLine: {
                                show: true,
                                lineStyle: {
                                    color: '#67a1e5'
                                }
                            },
                            axisLabel: {
                                formatter: '{value}'
                            },
                            splitLine: {
                                show: false
                            }
                        },
                        {
                            type: 'value',
                            name: '常住人口\n（万人）',
                            min: 0,
                            max: 3200,
                            position: 'left',
                            offset: 80,
                            axisLine: {
                                show: true,
                                lineStyle: {
                                    color: '#50e3c2'
                                }
                            },
                            axisLabel: {
                                formatter: '{value}'
                            },
                            splitLine: {
                                show: false
                            }
                        },
                        {
                            type: 'value',
                            name: 'GDP增速',
                            min: -5,
                            max: 5,
                            position: 'right',
                            axisLine: {
                                show: true,
                                lineStyle: {
                                    color: '#D0648A'
                                }
                            },
                            axisLabel: {
                                formatter: '{value}%'
                            },
                            splitLine: {
                                show: false
                            }
                        }
                    ],
                    series: [
                        {
                            name: 'GDP总量（亿元）',
                            type: 'bar',
                            data: [38701, 36103, 27670, 25019, 25003, 20171, 17717, 16106, 15616, 14818]
                        },
                        {
                            name: '常住人口（万人）',
                            type: 'bar',
                            yAxisIndex: 1,
                            data: [2428, 2154, 1344, 1531, 3124, 1075, 1658, 1036, 1121, 851]
                        },
                        {
                            name: 'GDP增速',
                            type: 'line',
                            yAxisIndex: 2,
                            data: [1.7, 1.2, 3.1, 2.7, 3.9, 3.4, 4.0, 3.9, -4.7, 4.6]
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