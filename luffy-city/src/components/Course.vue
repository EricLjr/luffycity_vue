<template>
  <div>
    <p>课程列表</p>
    <ul v-for="i in list">
      <li>{{i.name}}</li>
    </ul>
    <input type="text" placeholder="用户名" v-model="username">
    <input type="text" placeholder="密码" v-model="password">
    <button @click="tik">提交</button>
  </div>
</template>

<script>
  import qs from 'qs'
    export default {
        name: "course",
      data(){
          return {list:[11,22,33],
          username:'',
            password:'',
          }
      },
      mounted:function(){
          this.Init()
      },
      methods:{
          Init:function(){
            var that=this;
            this.$axios.request({
              url:'http://127.0.0.1:8000/api/v1/a/',
              method:'GET',
              responseType:'json'
            })
              .then(
                function (res) {
                  if(res.data.code===1000){
                    that.list=res.data.data
                  }else{
                    alert(123)
                  }
                }
              ).catch(function (error) {
              console.log(error.data)
            })
          },
        tik:function () {
          this.$axios.request({
            url:'http://127.0.0.1:8000/api/v1/auth/',
            method:'POST',
            responseType:'json',
            headers:{
              // 'Content-Type:':'application/json',
                  'ljr':123,
            },
            data:{
                  user:this.username,
                  pwd:this.password,
                },
          }).then(function (arg) {
                // 成功之后
                console.log(123);
              }).catch(function (arg) {

              })
        }
      }
    }
</script>

<style scoped>

</style>
