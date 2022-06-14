<template>
    <div class="common-table">
        <el-table :data="tableData" height="90%" stripe>
            <el-table-column
            show-overflow-tooltip
            v-for ="item in tableLabel"
            :key ="item.prop"
            :label ="item.label"
            :width ="item.width ? item.width : 125">
                <template slot-scope="scope">
                    <span style="margin-left :10px">{{ scope.row[item.prop] }}</span>
                </template>
            </el-table-column>
            <el-table-column label="操作" min-width="180">
                <template slot-scope="scope">
                <el-button size="mini" @click="handleEdit(scope.row)">编辑</el-button>
                <el-button size = "mini" @click="handleDelete(scope.row)">删除</el-button>
                </template>
            </el-table-column>
        </el-table>
        <el-pagination
            class="pager"
            layout="prev,pager,next"
            :total="config.total"
            :current-page.sync="config.page"
            @current-change="changePage"
            :page-size="20"></el-pagination>
    </div>
</template>

<script>
export default{
    name:"CommonTable",
    props:{
        tableData:Array,
        config:Object
    },
    data(){
        return {
        tableLabel:[
            {
                prop:"name",
                label:"姓名"
            },
            {
                prop:"age",
                label:"年龄"
            },
            {

                prop:"sexLabel",
                label:"性别"
            },
            {
                prop:"birth",
                label:"出生日期",
                width:200
            },
            {
                prop:"addr",
                label:"地址",
                width:320
            },
            ],
        }
    },
    methods:{
        handleEdit(row){
            this.$emit('edit',row)
        },
        handleDelete(row){
            this.$emit('del',row)
        },
        changePage(page){
            this.$emit("changePage",page)
        }
    }
    

}
</script>

<style lang="less" scoped>
    .common-table{
    height: calc(100% - 62px);
    background-color: #fff;
    position: relative;
    .pager{
        position: absolute;
        bottom:0;
    }
}
</style>