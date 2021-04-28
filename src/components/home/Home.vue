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
                        <a class="loginout" href="#">退出</a>
                    </div>
                </el-col>
            </el-row>

        </el-header>
        <el-container>
            <el-aside width="200px" class="aside">Aside</el-aside>
            <el-main class="main">Main</el-main>
        </el-container>
        </el-container>
    </div>
</template>

<script>
export default {

}
</script>

<style>
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
     background-color: #D3DCE6;
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