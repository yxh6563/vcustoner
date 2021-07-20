<template>
  <div class="customers container">
    <h1 class="page-header">用户管理系统</h1>
    <input type="text" placeholder="请输入内容" class="input_search" v-model="filterInput">
    <hr>
    <table class="imagetable" border="1">
      <tr>
        <td>姓名</td>
        <td>电话</td>
        <td>邮箱</td>
        <td>操作</td>
      </tr>
      <tr v-for="(customer,index) in filterBy" :key="index">
        <td>{{ customer.name }}</td>
        <td>{{ customer.phone }}</td>
        <td>{{ customer.email }}</td>
        <td>
          <router-link v-bind:to="'/customer/'+customer.id">详情</router-link>
        </td>
    </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: 'customers',
  data(){
    return{
      customers:[],
      filterInput:""
    }
  },
  methods:{
    submit(){
    this.$http.get("http://localhost:3000/userlist")
      .then(function(response){
        // console.log(response);
        this.customers = response.body;
      })
    }
  },
 computed: {
    filterBy() {
        return this.customers.filter(customer => {
            return customer.name.match(this.filterInput);
        })
    }
  },
  created(){
    this.submit();
  },
  updated(){
    this.submit();
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container{
  margin-left: 25px;
  margin-top: 20px;
}
table.imagetable {
		    font-family: verdana,arial,sans-serif;
		    font-size:11px;
		    color:#333333;
		    border-width: 1px;
		    border-color: #999999;
		    border-collapse: collapse;
        width: 100%;
        margin-top: 50px;
		}
		table.imagetable tr {
		    background:#b5cfd2;
		    border-width: 1px;
		    padding: 8px;
		    border-style: solid;
		    border-color: #999999;
		}
		table.imagetable td {
		    background:#dcddc0;
		    border-width: 1px;
		    padding: 8px;
		    border-style: solid;
		    border-color: #999999;
		}
.input_search{
  width: 80%;
}
</style>
