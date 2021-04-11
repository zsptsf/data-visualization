<template>
    <div>
        <Echart
                id="speed20"
                :options="options"
                height="4rem"
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
                    tooltip: {
                        trigger: 'item',
                        formatter: '{b}{a}{c}%'
                    },
                    series: [
                        {
                            name: '增速',
                            type: 'pie',
                            roseType: 'radius',
                            radius: '110%',
                            center:['50%','65%'],
                            label: {
                                position: 'inner',
                                formatter: '{b}{c}%',
                                fontSize: 14,
                                color:'#666'
                            },
                            data: [
                                {value: 12, name: '舟山'},
                                {value: 6.0, name: '楚雄'},
                                {value: 6.6, name: '曲靖'},
                                {value: 7.1, name: '怒江'},
                                {value: 7.9, name: '德宏'},
                                {value: 5.7, name: '博尔塔拉'},
                                {value: 5.9, name: '阿克苏'},
                                {value: 6.1, name: '晋城'},
                                {value: 6.8, name: '山南'},
                                {value: 6.0, name: '石嘴山'},
                                {value: 6.2, name: '吴忠'},
                                {value: 6.1, name: '崇左'},
                                {value: 6.3, name: '来宾'},
                                {value: 6.3, name: '百色'},
                                {value: 7.0, name: '贺州'},
                                {value: 7.0, name: '贵港'},
                                {value: 8.0, name: '梧州'},
                                {value: 6.0, name: '宁德'},
                                {value: 5.7, name: '厦门'},
                                {value: 8.7, name: '金昌'},
                                {value: 6.3, name: '酒泉'}
                            ]
                        }
                    ]
                },
            };
        },
        components: {
            Echart,
        },
        methods: {
        },
    }
</script>