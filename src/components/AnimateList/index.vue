<template>
    <div id="animateList">
        <el-table :data="List" class="hidden-tbody"
                  :header-cell-style="{background:'#07216a',borderColor:'#CECECE',color:'#fff'}">
            <el-table-column prop="id" label="排名" align="center" width="60"></el-table-column>
            <el-table-column prop="change" label="变化" align="center" width="60"></el-table-column>
            <el-table-column prop="name" label="地区" align="center" width="120"></el-table-column>
            <el-table-column prop="province" label="省份" align="center" width="90"></el-table-column>
            <el-table-column prop="value" label="GDP（亿元）" align="center"></el-table-column>
            <el-table-column prop="probability" label="实际增速（%）" align="center"></el-table-column>
        </el-table>
        <vueSeamlessScroll :data="List" :class-option="optionSingleHeight" class="auto-scorll-table">
            <el-table
                    :data="List"
                    class="hidden-thead"
                    :header-cell-style="{background:'#07216a',borderColor:'#CECECE',color:'#fff'}"
                    :row-style="{height:'38px',backgroundColor:'rgb(0,54,160)',color:'#fff'}"
                    :cell-style="{padding:'0px'}">
                <el-table-column prop="id" label="排名" align="center" width="60"></el-table-column>
                <el-table-column label="变化" align="center" width="60">
                    <template slot-scope="scope">
                        <p v-if="scope.row.change > 0" style="height: 36px;color: red;margin: 0px">↑ {{scope.row.change}}</p>
                        <p v-if="scope.row.change == 0" style="height: 36px;margin: 0px">-</p>
                        <p v-if="scope.row.change < 0" style="height: 36px;color: green;margin: 0px">↓ {{scope.row.change*-1}}</p>
                    </template>
                </el-table-column>
                <el-table-column prop="name" label="地区" align="center" width="120"></el-table-column>
                <el-table-column prop="province" label="省份" align="center" width="90"></el-table-column>
                <el-table-column prop="value" label="GDP（亿元）" align="center"></el-table-column>
                <el-table-column label="实际增速（%）" align="center">
                    <template slot-scope="scope">
                        <p v-if="scope.row.probability > 0" style="height: 36px;color: red;margin: 0px">{{scope.row.probability}}</p>
                        <p v-if="scope.row.probability == 0" style="height: 36px;margin: 0px">-</p>
                        <p v-if="scope.row.probability < 0" style="height: 36px;color: green;margin: 0px">{{scope.row.probability}}</p>
                    </template>
                </el-table-column>
            </el-table>
        </vueSeamlessScroll>
    </div>
</template>

<script>
    import vueSeamlessScroll from 'vue-seamless-scroll'
    export default {
        name: "animateList",
        components:{
            vueSeamlessScroll
        },
        computed: {
            optionSingleHeight () {
                return {
                    limitMoveNum: 0,
                    singleHeight: 38
                }
            }
        },
        props:{
            List: {
                type: Array,
                default: []
            },
        },
        data() {
            return {

            }
        },
        mounted() {

        },
        methods: {

        },
    }
</script>

<style scoped>
    .hidden-tbody.el-table {
        height: 48px;
        box-sizing: border-box;
        background-color: rgba(0,0,0,0.5);
    }
    .hidden-tbody.el-table tbody {
        display: none;
        overflow: hidden;
    }
    .auto-scorll-table {
        height: 3rem;
        overflow: hidden;
    }
    .auto-scorll-table .hidden-thead.el-table {
        border-top: none;
        margin-top: -48px;
    }
    .auto-scorll-table .hidden-thead.el-table thead {
        display: none;
        overflow: hidden;
    }
    /deep/ .el-table tbody tr:hover>td {
        background-color: rgb(2, 89, 228)
    }
</style>