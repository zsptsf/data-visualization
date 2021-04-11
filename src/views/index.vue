<template>
    <div class="index" :style ="note">
        <el-row>
            <el-col :xs="{span:12,offset:6}" :sm="{span:12,offset:6}" :md="{span:12,offset:6}" :lg="{span:16,offset:4}" :xl="{span:16,offset:4}">
                <div class="visualization">2020年中国GDP大数据可视图</div>
            </el-col>
            <el-col :xs="1" :sm="1" :md="1" :lg="1" :xl="1">
                <div @click="handleFullScreen" class="screen">
                    <el-tooltip v-if="fullscreen" effect="light" content="退出全屏" placement="bottom">
                        <i class="el-icon-copy-document"></i>
                    </el-tooltip>
                    <el-tooltip v-else effect="light" content="全屏" placement="bottom">
                        <i class="el-icon-full-screen"></i>
                    </el-tooltip>
                </div>
            </el-col>
            <el-col :xs="5" :sm="5" :md="5" :lg="3" :xl="3">
                <div class="time">{{date}}</div>
            </el-col>
        </el-row>
        <el-row>
            <el-col :xs="24" :sm="24" :md="24" :lg="8" :xl="8">
                <el-row>
                    <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="24">
                        <div :style ="box">
                            <div class="title"><i class="el-icon-s-data"></i> 2020年一线城市GDP榜</div>
                            <firstTierCity style="margin-top: -60px;"></firstTierCity>
                        </div>
                    </el-col>
                </el-row>
                <el-row>
                    <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12">
                        <div class="loopLeft">
                            <div class="title3"><i class="el-icon-s-help"></i> GDP增速20强城市</div>
                            <speed20></speed20>
                        </div>
                    </el-col>
                    <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12">
                        <div class="loopLeft">
                            <div class="title3"><i class="el-icon-s-help"></i> 珠三角城市群实力图</div>
                            <zsj></zsj>
                        </div>
                    </el-col>
                </el-row>
                <el-row>
                    <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12">
                        <div class="loopRight">
                            <div class="title3"><i class="el-icon-s-help"></i> 京津冀城市群实力图</div>
                            <jjj></jjj>
                        </div>
                    </el-col>
                    <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12">
                        <div class="loopRight">
                            <div class="title3"><i class="el-icon-s-help"></i> 长三角城市群实力图</div>
                            <csj></csj>
                        </div>
                    </el-col>
                </el-row>
            </el-col>
            <el-col :xs="24" :sm="12" :md="12" :lg="8" :xl="8">
                <Map style="margin: 0.125rem;"></Map>
            </el-col>
            <el-col :xs="24" :sm="12" :md="12" :lg="8" :xl="8">
                <div class="animatList">
                    <div class="title1"><i class="el-icon-s-grid"></i> 2020年城市GDP百强榜</div>
                    <AnimateList :List="List"></AnimateList>
                </div>
            </el-col>
            <el-col :xs="24" :sm="24" :md="24" :lg="16" :xl="16">
                <div class="top10">
                    <div class="title2"><i class="el-icon-s-marketing"></i> 2020年GDP十强城市</div>
                    <top10></top10>
                </div>
            </el-col>
        </el-row>
    </div>
</template>

<script>
    import Map from '@/components/map/index'
    import jjj from '@/components/region/jjj'
    import csj from '@/components/region/csj'
    import zsj from '@/components/region/zsj'
    import AnimateList from '@/components/AnimateList/index'
    import top10 from '@/components/top10/index'
    import speed20 from '@/components/speed20/index'
    import firstTierCity from '@/components/firstTierCity/index'

    export default {
        components:{
            Map,
            jjj,
            csj,
            zsj,
            AnimateList,
            top10,
            speed20,
            firstTierCity
        },
        data() {
            return {
                List:[
                    {id:1, change:0, name: '上海', province: '上海', value: 38701, probability: 1.7},
                    {id:2, change:0, name: '北京', province: '北京', value: 36103, probability: 1.2},
                    {id:3, change:0, name: '深圳', province: '广东', value: 27670, probability: 3.1},
                    {id:4, change:0, name: '广州', province: '广东', value: 25019, probability: 2.7},
                    {id:5, change:0, name: '重庆', province: '重庆', value: 25003, probability: 3.9},
                    {id:6, change:0, name: '苏州', province: '江苏', value: 20171, probability: 3.4},
                    {id:7, change:0, name: '成都', province: '四川', value: 17717, probability: 4.0},
                    {id:8, change:1, name: '杭州', province: '浙江', value: 16106, probability: 3.9},
                    {id:9, change:-1, name: '武汉', province: '湖北', value: 15616, probability: -4.7},
                    {id:10, change:1, name: '南京', province: '江苏', value: 14818, probability: 4.6},
                    {id:11, change:-1, name: '天津', province: '天津', value: 14084, probability: 1.5},
                    {id:12, change:0, name: '宁波', province: '浙江', value: 12409, probability: 3.3},
                    {id:13, change:1, name: '青岛', province: '山东', value: 12401, probability: 3.7},
                    {id:14, change:-1, name: '无锡', province: '江苏', value: 12370, probability: 3.7},
                    {id:15, change:1, name: '长沙', province: '湖南', value: 12143, probability: 4.0},
                    {id:16, change:-1, name: '郑州', province: '河南', value: 12003, probability: 3.0},
                    {id:17, change:0, name: '佛山', province: '广东', value: 10816, probability: 1.6},
                    {id:18, change:0, name: '泉州', province: '福建', value: 10159, probability: 2.9},
                    {id:19, change:1, name: '济南', province: '山东', value: 10141, probability: 4.9},
                    {id:20, change:1, name: '合肥', province: '安徽', value: 10046, probability: 4.3},
                    {id:21, change:2, name: '南通', province: '江苏', value: 10036, probability: 4.7},
                    {id:22, change:2, name: '西安', province: '陕西', value: 10020, probability: 5.2},
                    {id:23, change:-1, name: '福州', province: '福建', value: 10020, probability: 5.1},
                    {id:24, change:-5, name: '东莞', province: '广东', value: 9650, probability: 1.1},
                    {id:25, change:0, name: '烟台', province: '山东', value: 7816, probability: 3.6},
                    {id:26, change:0, name: '常州', province: '江苏', value: 7805, probability: 4.5},
                    {id:27, change:0, name: '徐州', province: '江苏', value: 7320, probability: 3.4},
                    {id:28, change:1, name: '唐山', province: '河北', value: 7211, probability: 4.4},
                    {id:29, change:-1, name: '大连', province: '辽宁', value: 7030, probability: 0.9},
                    {id:30, change:0, name: '温州', province: '浙江', value: 6871, probability: 3.4},
                    {id:31, change:0, name: '昆明', province: '云南', value: 6734, probability: 2.3},
                    {id:32, change:2, name: '长春', province: '吉林', value: 6638, probability: 3.6},
                    {id:33, change:-1, name: '沈阳', province: '辽宁', value: 6572, probability: 0.8},
                    {id:34, change:-1, name: '厦门', province: '福建', value: 6384, probability: 5.7},
                    {id:35, change:0, name: '扬州', province: '江苏', value: 6048, probability: 3.5},
                    {id:36, change:1, name: '绍兴', province: '浙江', value: 6001, probability: 3.3},
                    {id:37, change:1, name: '盐城', province: '江苏', value: 5953, probability: 3.5},
                    {id:38, change:-2, name: '石家庄', province: '河北', value: 5935, probability: 3.9},
                    {id:39, change:0, name: '潍坊', province: '山东', value: 5872, probability: 3.6},
                    {id:40, change:0, name: '南昌', province: '江西', value: 5746, probability: 3.6},
                    {id:41, change:0, name: '嘉兴', province: '浙江', value: 5510, probability: 3.5},
                    {id:42, change:1, name: '泰州', province: '江苏', value: 5313, probability: 3.6},
                    {id:43, change:-1, name: '台州', province: '浙江', value: 5263, probability: 3.4},
                    {id:44, change:0, name: '哈尔滨', province: '黑龙江', value: 5184, probability: 0.6},
                    {id:45, change:0, name: '洛阳', province: '河南', value: 5128, probability: 3.0},
                    {id:46, change:2, name: '临沂', province: '山东', value: 4805, probability: 3.9},
                    {id:47, change:0, name: '漳州', province: '福建', value: 4747, probability: -1.5},
                    {id:48, change:2, name: '南宁', province: '广西', value: 4726, probability: 3.7},
                    {id:49, change:0, name: '金华', province: '浙江', value: 4704, probability: 2.8},
                    {id:50, change:-4, name: '襄阳', province: '湖北', value: 4602, probability: -5.3},
                    {id:51, change:1, name: '济宁', province: '山东', value: 4494, probability: 3.6},
                    {id:52, change:4, name: '贵阳', province: '贵州', value: 4312, probability: 5.0},
                    {id:53, change:-2, name: '宜昌', province: '湖北', value: 4261, probability: -4.7},
                    {id:54, change:-1, name: '惠州', province: '广东', value: 4222, probability: 1.5},
                    {id:55, change:0, name: '镇江', province: '江苏', value: 4220, probability: 3.5},
                    {id:56, change:1, name: '太原', province: '山西', value: 4153, probability: 2.6},
                    {id:57, change:-3, name: '榆林', province: '陕西', value: 4090, probability: 4.5},
                    {id:58, change:0, name: '淮安', province: '江苏', value: 4025, probability: 3.2},
                    {id:59, change:1, name: '岳阳', province: '湖南', value: 4002, probability: 4.2},
                    {id:60, change:-1, name: '南阳', province: '河南', value: 3926, probability: 2.2},
                    {id:61, change:2, name: '芜湖', province: '安徽', value: 3753, probability: 3.4},
                    {id:62, change:0, name: '常德', province: '湖南', value: 3749, probability: 3.9},
                    {id:63, change:4, name: '遵义', province: '贵州', value: 3720, probability: 4.6},
                    {id:64, change:1, name: '沧州', province: '河北', value: 3700, probability: 4.1},
                    {id:65, change:-4, name: '淄博', province: '山东', value: 3674, probability: 2.5},
                    {id:66, change:2, name: '赣州', province: '江西', value: 3645, probability: 4.2},
                    {id:67, change:-1, name: '邯郸', province: '河北', value: 3637, probability: 4.3},
                    {id:68, change:-4, name: '鄂尔多斯', province: '内蒙古', value: 3534, probability: -2.9},
                    {id:69, change:4, name: '衡阳', province: '湖南', value: 3509, probability: 4.0},
                    {id:70, change:0, name: '乌鲁木齐', province: '新疆', value: 3500, probability: 0},
                    {id:71, change:0, name: '菏泽', province: '山东', value: 3483, probability: 3.9},
                    {id:72, change:-3, name: '珠海', province: '广东', value: 3482, probability: 3.0},
                    {id:73, change:-1, name: '许昌', province: '河南', value: 3449, probability: 2.7},
                    {id:74, change:1, name: '保定', province: '河北', value: 3353, probability: 0},
                    {id:75, change:2, name: '廊坊', province: '河北', value: 3301, probability: 3.5},
                    {id:76, change:-2, name: '茂名', province: '广东', value: 3279, probability: 1.5},
                    {id:77, change:2, name: '连云港', province: '江苏', value: 3277, probability: 3.0},
                    {id:78, change:-2, name: '周口', province: '河南', value: 3267, probability: 1.7},
                    {id:79, change:5, name: '宿迁', province: '江苏', value: 3262, probability: 4.5},
                    {id:80, change:2, name: '九江', province: '江西', value: 3241, probability: 3.8},
                    {id:81, change:0, name: '湖州', province: '浙江', value: 3201, probability: 3.3},
                    {id:82, change:-4, name: '江门', province: '广东', value: 3201, probability: 2.2},
                    {id:83, change:-3, name: '柳州', province: '广西', value: 3177, probability: 1.5},
                    {id:84, change:-1, name: '中山', province: '广东', value: 3152, probability: 1.5},
                    {id:85, change:2, name: '株洲', province: '湖南', value: 3106, probability: 4.1},
                    {id:86, change:-1, name: '湛江', province: '广东', value: 3100, probability: 1.9},
                    {id:87, change:-1, name: '德州', province: '山东', value: 3079, probability: 3.6},
                    {id:88, change:4, name: '滁州', province: '安徽', value: 3032, probability: 4.4},
                    {id:89, change:-1, name: '威海', province: '山东', value: 3018, probability: 3.0},
                    {id:90, change:-1, name: '新乡', province: '河南', value: 3015, probability: 3.2},
                    {id:91, change:2, name: '绵阳', province: '四川', value: 3010, probability: 4.4},
                    {id:92, change:-2, name: '东营', province: '山东', value: 2981, probability: 3.8},
                    {id:93, change:12, name: '曲靖', province: '云南', value: 2959, probability: 6.6},
                    {id:94, change:-3, name: '商丘', province: '河南', value: 2925, probability: -0.8},
                    {id:95, change:-1, name: '兰州', province: '甘肃', value: 2887, probability: 2.4},
                    {id:96, change:7, name: '龙岩', province: '福建', value: 2871, probability: 5.3},
                    {id:97, change:1, name: '驻马店', province: '河南', value: 2859, probability: 3.6},
                    {id:98, change:-1, name: '信阳', province: '河南', value: 2806, probability: 2.1},
                    {id:99, change:1, name: '阜阳', province: '安徽', value: 2805, probability: 3.8},
                    {id:100, change:6, name: '宜宾', province: '四川', value: 2802, probability: 4.6},
                ],
                note: {
                    backgroundImage: "url(" + require("../assets/img/bg.jpg") + ")",
                    backgroundSize: "100% 100%",
                },
                box: {
                    margin:"10px 10px 10px 10px",
                    height: "2rem",
                    border: "0.25rem solid transparent",
                    borderImage: "url("+require("../assets/img/border.png")+") 51 32 18 66",
                },
                date: new Date(),
                fullscreen: false,
            };
        },
        mounted(){
            let that= this;
            this.timer = setInterval(function() {
                that.date = new Date().toLocaleString();
            });
        },
        methods:{
            // 全屏事件
            handleFullScreen() {
                let element = document.documentElement;
                if (this.fullscreen) {
                    if (document.exitFullscreen) {
                        document.exitFullscreen();
                    } else if (document.webkitCancelFullScreen) {
                        document.webkitCancelFullScreen();
                    } else if (document.mozCancelFullScreen) {
                        document.mozCancelFullScreen();
                    } else if (document.msExitFullscreen) {
                        document.msExitFullscreen();
                    }
                } else {
                    if (element.requestFullscreen) {
                        element.requestFullscreen();
                    } else if (element.webkitRequestFullScreen) {
                        element.webkitRequestFullScreen();
                    } else if (element.mozRequestFullScreen) {
                        element.mozRequestFullScreen();
                    } else if (element.msRequestFullscreen) {
                        // IE11
                        element.msRequestFullscreen();
                    }
                }
                this.fullscreen = !this.fullscreen;
            },
        },
        beforeDestroy: function() {
            if (this.timer) {clearInterval(this.timer);}
        }
    }
</script>

<style scoped>
    .index {

    }
    .visualization{
        color: #377ee5;
        font-size: 17px;
        font-weight: bold;
        margin-bottom: 15px;
        text-align: center;
        margin-top: 0.125rem;
    }
    .screen{
        margin-top: 0.125rem;
        font-size: 17px;
        color: #fff;
        cursor:pointer
    }
    .time{
        margin-top: 0.125rem;
        font-size: 14px;
        color: #fff
    }
    .title{
        color: #377ee5;
        font-size: 17px;
        font-weight: bold;
        margin-bottom: 15px;
    }
    .title1{
        color: #377ee5;
        font-size: 17px;
        font-weight: bold;
        text-align: center;
        margin: 15px 0;
    }
    .title2{
        color: #377ee5;
        font-size: 17px;
        font-weight: bold;
        text-align: center;
    }
    .title3{
        color: #377ee5;
        font-size: 14px;
        text-align: center;
    }
    .animatList{
        border-radius:10px;
        background-color: rgba(0,0,0,0.2);
        padding: 10px;
    }
    .top10{
        border-radius:10px;
        height: 5.6rem;
        background-color: rgba(0,0,0,0.2);
        padding: 10px 0;
        margin-top: 0.25rem;
    }
</style>
