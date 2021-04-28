<template>
  <el-card class="box-card">
      <!-- 面包屑 -->
        <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item >首页</el-breadcrumb-item>
            <el-breadcrumb-item>用户管理</el-breadcrumb-item>
            <el-breadcrumb-item>用户列表</el-breadcrumb-item>
        </el-breadcrumb>
      <!-- 搜索 -->
      <el-row class="searceRow">
          <el-col>
               <el-input placeholder="请输入内容" v-model="query" class="inputSearch"> 
                    <el-button slot="append" icon="el-icon-search"></el-button>
                </el-input>
                <el-button type="primary">添加用户</el-button>

                <!-- 表格 -->
                <el-table
                    class="table-box"
                    :data="tableData"
                    border
                    style="width: 100%"
                    :row-class-name="tableRowClassName">
                    <el-table-column
                        type="index"
                        label="#"
                        width="60">
                    </el-table-column>
                    <el-table-column
                        prop="name"
                        label="姓名"
                        width="180">
                    </el-table-column>
                    <el-table-column
                        prop="email"
                        label="邮箱"
                        width="180">
                    </el-table-column>
                     <el-table-column
                        prop="phone"
                        label="电话"
                        width="180">
                    </el-table-column>
                     <el-table-column
                        prop="createTime"
                        label="创建时间"
                        width="180">
                    </el-table-column>
                     <el-table-column
                        prop="state"
                        label="用户状态"
                        width="180">
                    </el-table-column>
                     <el-table-column
                        prop="operation"
                        label="操作"
                        width="180">
                    </el-table-column>
                </el-table>
          </el-col>
      </el-row>

      

      <!-- 分页 -->
  </el-card>
</template>

<script>
export default {
    data(){
        return {
            query:'',
            tableData: [{
                date: '2016-05-02',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1518 弄',
                }, {
                date: '2016-05-04',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1518 弄'
                }, 
            ]
        }
    },
     methods: {
      tableRowClassName({row, rowIndex}) {
        if (rowIndex === 1) {
          return 'warning-row';
        } else if (rowIndex === 3) {
          return 'success-row';
        }
        return '';
      }
    },
}
</script>

<style>
.box-card{
    height: 100%;
}
.inputSearch{
    
    width: 400px;
}
.searceRow{
    margin-top: 20px;
}
.table-box{
    margin-top: 20px;
}
</style>