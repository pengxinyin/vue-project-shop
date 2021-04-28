<template>
  <div class="login-wrap">
    <el-form 
    class="login-form"
    label-position="top" 
    label-width="80px" 
    :model="formdata">
        <h2>用户登录</h2>
        <el-form-item label="用户名">
            <el-input v-model="formdata.username"></el-input>
        </el-form-item>
        <el-form-item label="密  码">
            <el-input v-model="formdata.password" type="password"></el-input>
        </el-form-item>
        <el-button
            @click.prevent= "handleLogin()"
            class="login-btn" type="primary">登录</el-button>
    </el-form>
  </div>
</template>

<script>
export default {
    data(){
        return {
            formdata:{
                username:'',
                password:''
            }
        }
    },
    methods:{
        // 登录请求
        // 让异步操作的代码  看起来像同步代码  async await
       async handleLogin(){
           // 异步操作
           const res = await this.$http.post('/login',this.formdata)
                // console.log(res);
                const {data,meta:{msg,status}} = res.data
                // 登录成功 跳转首页 提示成功
                if(status === 200){
                    // 跳转首页
                    this.$router.push({name:'home'})
                    // 提示成功
                     this.$message.success(msg)
                }else{
                    // 登录不成功  不成功提示
                    this.$message.error(msg);
                }

        //     this.$http.post('/login',this.formdata).then(res=>{
        //         // console.log(res);
        //         const {data,meta:{msg,status}} = res.data

        //         // 登录成功 跳转首页 提示成功
        //         if(status === 200){
        //             // 跳转首页
        //             this.$router.push({name:'home'})
        //             // 提示成功
        //              this.$message.success(msg)
        //         }else{
        //             // 登录不成功  不成功提示
        //             this.$message.error(msg);
        //         }
                
        //     })
        }
    }
}
</script>

<style>

.login-wrap{
    height: 100%;
    background-color: #324152;
    /* 弹性布局 */
    display: flex;
    justify-content: center;
    align-items: center;
}
.login-wrap .login-form{
    width: 450px;
    background-color: #fff;
    border-radius: 5px;
    padding: 30px;
}
.login-wrap .login-btn{
    width: 100%;
}
</style>