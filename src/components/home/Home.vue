<template>
    <div class="home">
       <el-container class="container">
        <el-header class="header">
            <el-row>
                <el-col :span="4">
                    <div class="grid-content bg-purple">
                        <img src="../../assets/logo.png" alt="无法显示图片"> 
                    </div>
                </el-col>
                <el-col :span="18" class="middle">
                    <h3>电商后台管理系统</h3>
                </el-col>
                <el-col :span="2">
                    <div class="grid-content bg-purple">
                        <a class="loginout" href="#" @click.prevent="handleLoginout()">退出</a>
                    </div>
                </el-col>
            </el-row>

        </el-header>
        <!-- 侧边栏导航开始 -->
        <el-container>
            <el-aside width="200px" class="aside">
                <!-- 开启路由模式为true:router="true" -->
                 <el-menu :router="true" :unique-opened="true">
                    <el-submenu index="1">
                        <template slot="title">
                            <i class="el-icon-user-solid"></i>
                            <span>用户管理</span>
                        </template>
                        <el-menu-item-group>
                             <el-menu-item index="users">
                                <i class="el-icon-edit"></i>
                                <span>用户列表</span>
                            </el-menu-item>
                        
                        </el-menu-item-group>
                    </el-submenu>
                    <el-submenu index="2">
                        <template slot="title">
                            <i class="el-icon-s-help"></i>
                            <span>权限管理</span>
                        </template>
                        <el-menu-item-group>
                             <el-menu-item index="1-2">
                                <i class="el-icon-location"></i>
                                <span>角色列表</span>
                            </el-menu-item>
                            
                            <el-menu-item index="1-2">
                                <i class="el-icon-location"></i>
                                <span>权限列表</span>
                            </el-menu-item>
                        </el-menu-item-group>    
                    </el-submenu>
                      <el-submenu index="3">
                        <template slot="title">
                            <i class="el-icon-shopping-bag-2"></i>
                            <span>商品管理</span>
                        </template>
                        <el-menu-item-group>
                             <el-menu-item index="1-2">
                                <i class="el-icon-location"></i>
                                <span>商品列表</span>
                            </el-menu-item>
                            
                            <el-menu-item index="1-2">
                                <i class="el-icon-notebook-1"></i>
                                <span>分类参数</span>
                            </el-menu-item>
                             <el-menu-item index="1-2">
                                <i class="el-icon-location"></i>
                                <span>商品分类</span>
                            </el-menu-item>
                        </el-menu-item-group> 
                    </el-submenu>
                      <el-submenu index="4">
                        <template slot="title">
                            <i class="el-icon-edit"></i>
                            <span>订单管理</span>
                        </template>
                        <el-menu-item-group>
                             <el-menu-item index="1-2">
                                <i class=""></i>
                                <span>订单列表</span>
                            </el-menu-item>
                            
                            <el-menu-item index="1-2">
                                <i class="el-icon-location"></i>
                                <span>选项2</span>
                            </el-menu-item>
                        </el-menu-item-group> 
                    </el-submenu>
                      <el-submenu index="5">
                        <template slot="title">
                            <i class="el-icon-pie-chart"></i>
                            <span>数据统计</span>
                        </template>
                        <el-menu-item-group>
                             <el-menu-item index="1-2">
                                <i class="el-icon-date"></i>
                                <span>数据报表</span>
                            </el-menu-item>
                            
                            <el-menu-item index="1-2">
                                <i class="el-icon-location"></i>
                                <span>选项2</span>
                            </el-menu-item>
                        </el-menu-item-group>  
                    </el-submenu>
                 </el-menu>


            </el-aside>
            <el-main class="main">
                <router-view></router-view>
            </el-main>
        </el-container>
        </el-container>
    </div>
</template>

<script>
export default {

    //new Vue 之前自动触发
    beforeCreate(){
        // 获取token
        const token = localStorage.getItem('token')
        // console.log(token);
        
        // token没有-》登录
        if(!token){
            this.$router.push('/login')
        }
        // 如果有就继续渲染组件
        
    },
    methods:{
        handleLoginout(){
            // 1.清楚token
            localStorage.clear()
            // 2.提示
            this.$message.success('退出成功')
            // 3.跳转到login组件
            this.$router.push('/login')
        }
    }
}
</script>

<style>
.home{
    height: 100% ;
}
.container{
     height: 100% ;
}
.header{
    background-color: #B3C0D1;
}
.header img{
    width: 100px;
    height: 60px;
    border-radius: 50%;
    
}
.aside{
    background-color: #fff
   
}
.main{
    background-color: #E9EEF3;
    
}

/* 头部样式开始 */
.middle{
    text-align: center;
    color: #fff;
}
.loginout{
    line-height: 60px;
    text-decoration: none;
}
</style>