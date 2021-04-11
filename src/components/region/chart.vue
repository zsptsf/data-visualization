<template>
      <div>
            <Echart
                :options="options"
                :id="chartID"
                height="4rem"
            ></Echart>
      </div>
</template>

<script>
import Echart from '@/common/echart'
export default {
    data () {
        return {
            options: {},
        };
    },
    components: {
        Echart,
    },
    props: {
        chartID: {
            type: String,
            default: 'chart'
        },
        cdata: {
            type: Object,
            default: () => ({})
        },
    },
    watch: {
        cdata: {
            handler (newData) {
                this.options = {
                    tooltip: {
                        trigger: 'item',
                        formatter: '{a} <br/>{b}: {c}'
                    },
                    title: [
                        {
                            subtext: '全国常住人口比例',
                            left: '33%',
                            top: '45%',
                            textAlign: 'center',
                            subtextStyle:{
                                color:'#eaeaea',
                                fontSize:10
                            },
                        }, {
                            subtext: '全国占地面积比例',
                            left: '50%',
                            top: '17%',
                            textAlign: 'center',
                            subtextStyle:{
                                color:'#eaeaea',
                                fontSize:10
                            },
                        }, {
                            subtext: '全国GDP总量占比',
                            left: '65%',
                            top: '45%',
                            textAlign: 'center',
                            subtextStyle:{
                                color:'#eaeaea',
                                fontSize:10
                            },
                        }
                    ],
                    series: [
                        {
                            name: '全国常住人口比例',
                            type: 'pie',
                            selectedMode: 'single',
                            top:'25%',
                            right:'30%',
                            radius: [0, '20%'],
                            label: {
                                show:false
                            },
                            labelLine: {
                                show: false
                            },
                            tooltip: {
                                trigger: 'item',
                                formatter: function(data){
                                    return data.name+"<br/>"+data.value+"亿人("+data.percent+"%)";
                                }
                            },
                            data: newData.populationData,
                        },
                        {
                            name: '全国占地面积比例',
                            type: 'pie',
                            selectedMode: 'single',
                            bottom:'30%',
                            radius: [0, '20%'],
                            label: {
                                show:false
                            },
                            labelLine: {
                                show: false
                            },
                            tooltip: {
                                trigger: 'item',
                                formatter: function(data){
                                    return data.name+"<br/>"+data.value+"万平方公里("+data.percent+"%)";
                                }
                            },
                            data: newData.areaData,
                        },
                        {
                            name: '全国GDP总量占比',
                            type: 'pie',
                            selectedMode: 'single',
                            top:'25%',
                            left:'30%',
                            radius: [ 0, '20%'],
                            label: {
                                show:false
                            },
                            labelLine: {
                                show: false
                            },
                            tooltip: {
                                trigger: 'item',
                                formatter: function(data){
                                    return data.name+"<br/>"+data.value+"万亿元("+data.percent+"%)";
                                }
                            },
                            data: newData.GDPData,
                        },
                        {
                            name: 'GDP总量',
                            type: 'pie',
                            radius: ['65%', '85%'],
                            labelLine: {
                                length: 20,
                            },
                            label: {
                                position: 'inner',
                                color:'#666'
                            },
                            data: newData.seriesData,
                        }
                    ]
                }
            },
            immediate: true,
            deep: true
        }
    }
};
</script>