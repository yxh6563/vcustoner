<template>
  <div class="edit container">
   <h1>编辑用户</h1>
   <el-form ref="form" :model="form" label-width="80px">
  <el-form-item label="姓名">
    <el-input v-model="form.name" placeholder="name"></el-input>
  </el-form-item>
  <el-form-item label="电话">
    <el-input v-model="form.phone" placeholder="phone"></el-input>
  </el-form-item>
   <el-form-item label="邮箱">
    <el-input v-model="form.email" placeholder="email"></el-input>
  </el-form-item>
   <el-form-item label="学历">
    <el-input v-model="form.education" placeholder="education"></el-input>
  </el-form-item>
   <el-form-item label="毕业学校">
    <el-input v-model="form.graduactionschool" placeholder="graduactionschool"></el-input>
  </el-form-item>
   <el-form-item label="职业">
    <el-input v-model="form.profession" placeholder="profession"></el-input>
  </el-form-item>
  <el-form-item label="个人简介">
    <el-input type="textarea" v-model="form.profile"></el-input>
  </el-form-item>
  <el-form-item>
    <el-button type="primary" v-on:click="submit" :plain="true">编辑</el-button>
    <el-button>取消</el-button>
  </el-form-item>
</el-form>
  </div>
</template>

<script>
export default {
  name: 'add',
  data(){
      return{
          form:{
              name:'',
              phone:'',
              email:'',
              education:'',
              graduactionschool:'',
              profession:'',
              profile:''
          },
          id:this.$route.params.id
      }
  },
  methods:{
      submit:function(){
          if(!this.form.name || !this.form.phone || !this.form.email){
              alert("请添加对应信息");
          }else{
              let updatedata = {
                  name: this.form.name,
                  phone: this.form.phone,
                  email: this.form.email,
                  education: this.form.education,
                  graduactionschool: this.form.graduactionschool,
                  profession: this.form.profession,
                  profile: this.form.profile
              }
              this.$http.put("http://localhost:3000/userlist/"+this.id,updatedata)
              .then(function(response){
                this.$message({
                       showClose: true,
                       message: '用户更新信息成功！',
                       type: 'success'
        });
                this.$router.push({path:"/",query:{alert:"sucess"}});
              })
          }
      }
  },
  created(){
      this.$http.get("http://localhost:3000/userlist/"+this.id)
      .then(function(response){
          this.form = response.body;
      })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container{
  margin-left: 25px;
  margin-top: 20px;
}
</style>