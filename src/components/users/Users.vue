<template>
  <el-card class="box-card">
      <!-- 面包屑 -->
        <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item >首页</el-breadcrumb-item>
            <el-breadcrumb-item>用户管理</el-breadcrumb-item>
            <el-breadcrumb-item>用户列表</el-breadcrumb-item>
        </el-breadcrumb>
      <!-- 搜索 -->
      <el-row class="searceRow" style="width:71%">
          <el-col>
               <el-input placeholder="请输入内容" v-model="query" class="inputSearch"> 
                    <el-button @click="searchUser()"  slot="append" icon="el-icon-search"></el-button>
                </el-input>
                <el-button type="primary">添加用户</el-button>

                <!-- 表格 -->
                <el-table
                    class="table-box"
                    :data="userslist"
                    border
                    style="width: 100%"
                   >
                    <el-table-column
                        type="index"
                        label="#"
                        width="60">
                    </el-table-column>
                    <el-table-column
                        prop="username"
                        label="姓名"
                        width="180">
                    </el-table-column>
                    <el-table-column
                        prop="email"
                        label="邮箱"
                        width="180">
                    </el-table-column>
                     <el-table-column
                        prop="mobile"
                        label="电话"
                        width="180">
                    </el-table-column>

                     <el-table-column
                        prop="create_time"
                        label="创建时间"
                        width="189">
                        <!-- 如果单元格内显示的内容不是字符串(文本)，粗腰个被显示的内容外层包裹一个template -->
                       
                       <!-- template 内部要用数据  设置slot-scope属性
                       该属性的值是需要用数据create_time的数据源userslist -->

                       <!-- slot-scope 的值userlist其实就是el-table绑定的数据userslist 
                       userslist.row 数据中的每个对象 -->
                        <template slot-scope="userslist">
                            {{userslist.row.create_time | fmtdate}}
                        </template>
                    </el-table-column>

                     <el-table-column
                        prop="mg_state"
                        label="用户状态"
                        width="180">
                        <template slot-scope="scope">
                            <el-switch
                                v-model="scope.row.mg_state"
                                active-color="#13ce66"
                                inactive-color="#ff4949">
                            </el-switch>
                        </template>
                        
                    </el-table-column>
                     <el-table-column
                        prop="operation"
                        label="操作"
                        width="180">
                        <!-- <template slot-scope="scope"> -->
                            
                                <el-button size="mini" plain type="primary" icon="el-icon-edit" circle></el-button>
                                <el-button size="mini" plain type="danger" icon="el-icon-delete" circle></el-button>
                                <el-button size="mini" plain type="success" icon="el-icon-check" circle></el-button>
                            
                        <!-- </template> -->
                    </el-table-column>
                </el-table>

                <!-- 分页 -->
                 <el-pagination
                    @size-change="handleSizeChange"
                    @current-change="handleCurrentChange"
                    :current-page="pagenum"
                    :page-sizes="[2, 4,6, 8]"
                    :page-size="2"
                    layout="total, sizes, prev, pager, next, jumper"
                    :total="total">
                    </el-pagination>
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
            // 表格绑定数据
            userslist: [],
             // 分页相关数据
             total:-1,
             pagenum:1,
             pagesize:2,
        }
    },
    created(){
        this.getUserList();
    },
    methods: {

        // 搜索用户
        searchUser(){
            // 按照input绑定的query参数发请求
            this.getUserList()
        },


        handleSizeChange(val) {
            this.pagesize = val
            
            this.getUserList()
            // console.log(`每页 ${val} 条`);
        },
        handleCurrentChange(val) {
            // console.log(`当前页: ${val}`); 
            this.pagenum = val
            this.getUserList()
        },
        async  getUserList(){
            //query 查询参数  可以为空
            // pagenum 当前页码  不能为空
            // pagesize  每页显示条数 不能为空
            // 不能拿数据的原因 后端文档接口 需要授权的 API ，必须在请求头中使用 `Authorization` 字段提供 `token` 令牌
            const AUTH_TOKEN = localStorage.getItem('token')
            this.$http.defaults.headers.common['Authorization'] = AUTH_TOKEN
            const res = await this.$http.get(`/users?query=${this.query}&pagenum=${this.pagenum}&pagesize=${this.pagesize}`)

            // console.log(res);
            const {meta:{status,msg},data:{users,total}} = res.data
            if(status === 200){
                // 给表格数据赋值
                this.userslist = users
                // console.log(this.userslist);
                // 给total赋值
                this.total = total
                // 提示
                this.$message.success(msg)
            }else{
                // 提示
                this.$message.error(msg)
            }
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