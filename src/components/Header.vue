<template>
  <header id="header">
   <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal">
  <el-menu-item>用户管理系统</el-menu-item>
  <el-menu-item index="1"><router-link to="/">主页</router-link></el-menu-item>
  <el-menu-item index="2"><router-link to="/about">关于我们</router-link></el-menu-item>
  <el-menu-item><router-link to="/add">添加用户</router-link></el-menu-item>
</el-menu>
    <router-view />
  </header>
</template>

<script>
export default {
  name: 'Header',
   data() {
      return {
        activeIndex: '1'
      };
    },
}
</script>

<style>

</style>
