<template>
  <div class="details container">
  <router-link to="/"><button>返回</button></router-link>
  <h1>{{customer.name}}
   <span class="pull-right">
             <router-link v-bind:to="'/edit/'+customer.id">
               <button class="edit">编辑</button>
             </router-link>
               <button class="del" v-on:click="delCustomer(customer.id)">删除</button>
         </span>
    </h1>
      <p><i class="iconfont icon-phone">
          <span>电话:{{customer.phone}}</span>
         </i>
      </p>
      <p><i class="iconfont icon-email">
          <span>邮箱:{{customer.email}}</span>
          </i>
      </p>
      <p><i class="iconfont icon-education">
          <span>教育:{{customer.education}}</span>
          </i>
      </p>
      <p><i class="iconfont icon-jixutubiao">
          <span>毕业学校:{{customer.graduactionschool}}</span>
          </i>
      </p>
      <p><i class="iconfont icon-profession">
          <span>职业:{{customer.profession}}</span>
          </i>
      </p>
  </div>
</template>

<script>
export default {
  name: 'customerdetails',
  data(){
    return{
      customer:{},
      id:this.$route.params.id
    }
  },
  created(){
      this.$http.get("http://localhost:3000/userlist/"+this.id)
      .then(function(response){
          console.log(response);
          this.customer = response.body;
      })
  },
  methods:{
      delCustomer:function(id){
        //   console.log(id);
        this.$http.delete("http://localhost:3000/userlist/"+this.id)
        .then(function(response){
             this.$message({
                       showClose: true,
                       message: '用户删除成功！',
                       type: 'success'
        });
            this.$router.push({path:"/",query:{alert:"sucess"}});
        })
      }
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container{
  margin-left: 25px;
  margin-top: 20px;
}
.iconfont{
    font-size: 25px;
}
span{
    margin-left: 13px;
}
.edit{
    background: blue;
    color: #fff;
    margin-left: 350px;
}
.del{
    background: crimson;
    color: #fff;
     margin-left: 20px;
}
</style>
