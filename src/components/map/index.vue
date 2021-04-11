<template>
    <div class="echart" ref="mapRef" id="map"></div>
</template>

<script>
    import chinaCityJson from './china-cities.json'
    import resizeMixins from '@/utils/resizeMixins'

    export default {
        name: "index",
        mixins: [resizeMixins],
        data(){
            return{
                data:[
                    {name: '上海', value: 38701},
                    {name: '北京', value: 36103},
                    {name: '深圳', value: 27670},
                    {name: '广州', value: 25019},
                    {name: '重庆', value: 25003},
                    {name: '苏州', value: 20171},
                    {name: '成都', value: 17717},
                    {name: '杭州', value: 16106},
                    {name: '武汉', value: 15616},
                    {name: '南京', value: 14818},
                    {name: '天津', value: 14084},
                    {name: '宁波', value: 12409},
                    {name: '青岛', value: 12401},
                    {name: '无锡', value: 12370},
                    {name: '长沙', value: 12143},
                    {name: '郑州', value: 12003},
                    {name: '佛山', value: 10816},
                    {name: '泉州', value: 10159},
                    {name: '济南', value: 10141},
                    {name: '合肥', value: 10046},
                    {name: '南通', value: 10036},
                    {name: '西安', value: 10020},
                    {name: '福州', value: 10020},
                    {name: '东莞', value: 9650},
                    {name: '烟台', value: 7816},
                    {name: '常州', value: 7805},
                    {name: '徐州', value: 7320},
                    {name: '唐山', value: 7211},
                    {name: '大连', value: 7030},
                    {name: '温州', value: 6871},
                    {name: '昆明', value: 6734},
                    {name: '长春', value: 6638},
                    {name: '沈阳', value: 6572},
                    {name: '厦门', value: 6384},
                    {name: '扬州', value: 6048},
                    {name: '绍兴', value: 6001},
                    {name: '盐城', value: 5953},
                    {name: '石家庄', value: 5935},
                    {name: '潍坊', value: 5872},
                    {name: '南昌', value: 5746},
                    {name: '嘉兴', value: 5510},
                    {name: '泰州', value: 5313},
                    {name: '台州', value: 5263},
                    {name: '哈尔滨', value: 5184},
                    {name: '洛阳', value: 5128},
                    {name: '临沂', value: 4805},
                    {name: '漳州', value: 4747},
                    {name: '南宁', value: 4726},
                    {name: '金华', value: 4704},
                    {name: '襄阳', value: 4602},
                    {name: '济宁', value: 4494},
                    {name: '贵阳', value: 4312},
                    {name: '宜昌', value: 4261},
                    {name: '惠州', value: 4222},
                    {name: '镇江', value: 4220},
                    {name: '太原', value: 4153},
                    {name: '榆林', value: 4090},
                    {name: '淮安', value: 4025},
                    {name: '岳阳', value: 4002},
                    {name: '南阳', value: 3926},
                    {name: '芜湖', value: 3753},
                    {name: '常德', value: 3749},
                    {name: '遵义', value: 3720},
                    {name: '沧州', value: 3700},
                    {name: '淄博', value: 3674},
                    {name: '赣州', value: 3645},
                    {name: '邯郸', value: 3637},
                    {name: '鄂尔多斯', value: 3534},
                    {name: '衡阳', value: 3509},
                    {name: '乌鲁木齐', value: 3500},
                    {name: '菏泽', value: 3483},
                    {name: '珠海', value: 3482},
                    {name: '许昌', value: 3449},
                    {name: '保定', value: 3353},
                    {name: '廊坊', value: 3301},
                    {name: '茂名', value: 3279},
                    {name: '连云港', value: 3277},
                    {name: '周口', value: 3267},
                    {name: '宿迁', value: 3262},
                    {name: '九江', value: 3241},
                    {name: '湖州', value: 3201},
                    {name: '江门', value: 3201},
                    {name: '柳州', value: 3177},
                    {name: '中山', value: 3152},
                    {name: '株洲', value: 3106},
                    {name: '湛江', value: 3100},
                    {name: '德州', value: 3079},
                    {name: '滁州', value: 3032},
                    {name: '威海', value: 3018},
                    {name: '新乡', value: 3015},
                    {name: '绵阳', value: 3010},
                    {name: '东营', value: 2981},
                    {name: '曲靖', value: 2959},
                    {name: '商丘', value: 2925},
                    {name: '兰州', value: 2887},
                    {name: '龙岩', value: 2871},
                    {name: '驻马店', value: 2859},
                    {name: '信阳', value: 2806},
                    {name: '阜阳', value: 2805},
                    {name: '宜宾', value: 2802},
                ],
                chart:null,
            }
        },
        watch: {
            options: {
                handler (options) {
                    // 设置true清空echart缓存
                    this.chart.setOption(options, true)
                },
                deep: true
            }
        },
        mounted() {
            this.initChart();
            this.handleMapRandomSelect();
        },
        beforeDestroy() {
            if (this.timer) {clearInterval(this.intervalId);}
        },
        methods: {
            initChart() {
                let that = this;
                this.chart = this.$echarts.init(document.getElementById('map'), 'shine');
                this.$echarts.registerMap("china", chinaCityJson);
                // 指定图表的配置项和数据
                let options = {
                    title: {
                        text: '2020年中国城市GDP百强图',
                        subtext: '21世纪经济报道',
                        sublink: 'https://baijiahao.baidu.com/s?id=1696189263765607901&wfr=spider&for=pc',
                        textStyle:{
                            color:'#377ee5'
                        },
                        subtextStyle:{
                            color:'#c7d5d9'
                        }
                    },
                    tooltip: {
                        textStyle: {
                            fontSize: '14px',
                        },
                        formatter: function(data){
                            if(!isNaN(data.value)){
                                return data.name+"<br/>"+data.value+"亿元";
                            }else{
                                return data.name
                            }
                        }
                    },
                    visualMap: {
                        orient: 'horizontal',
                        min: 2800,
                        max: 38800,
                        text: ['GDP(亿元)'],
                        realtime: false,
                        calculable: true,
                        inRange: {
                            color: ['lightskyblue', 'yellow', 'orangered']
                        },
                        textStyle:{
                            color:'#fff'
                        },
                    },
                    series: [
                        {
                            name:'2020年中国城市GDP百强榜',
                            type: "map",
                            roam: true,
                            map: "china",
                            itemStyle: {
                                areaColor: "#1f8bcb",
                                borderColor: "#739af5",
                                borderWidth: 1
                            },
                            emphasis: {
                                label: {
                                    show: false
                                },
                                itemStyle: {
                                    areaColor: "#f59a05"
                                }
                            },
                            data:[...this.data]
                        },
                    ]
                };
                this.chart.setOption(options, true);
            },
            // 开启定时器
            startInterval() {
                if (this.intervalId !== null) {
                    clearInterval(this.intervalId);
                }
                this.intervalId = setInterval(() => {
                    this.reSelectMapRandomArea();
                }, 2000);
            },
            // 重新随机选中地图区域
            reSelectMapRandomArea() {
                this.$nextTick(() => {
                    let index = Math.floor(Math.random() * this.data.length);
                    this.chart.dispatchAction({
                        type: 'showTip',
                        seriesIndex: 0,
                        dataIndex: index,
                    });
                    this.chart.dispatchAction({
                        type: 'select',
                        seriesIndex: 0,
                        dataIndex: index,
                    });
                });
            },
            handleMapRandomSelect() {
                this.$nextTick(() => {
                    setTimeout(() => {
                        this.reSelectMapRandomArea();
                    }, 0);
                    // 移入区域，清除定时器、取消之前选中并选中当前
                    this.chart.on('mouseover', (params)=> {
                        clearInterval(this.intervalId);
                    });
                    // 移出区域重新随机选中地图区域，并开启定时器
                    this.chart.on('globalout', ()=> {
                        this.reSelectMapRandomArea();
                        this.startInterval();
                    });
                    this.startInterval();
                });
            },
        }
    }
</script>

<style scoped>
    .echart {
        height: 4.5rem;
    }
</style>
