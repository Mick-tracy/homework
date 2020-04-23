<template>
  <div class="header">
    <h1>待办事项</h1>
    <div id="nav">
      <router-link to="/">主页</router-link>
      <router-link to="/about">关于</router-link>
    </div>
  </div>
  
</template>

<script>
export default {
  name: 'Header',
}
</script>

<style scoped>
.header {
  background: #333;
  color: #fff;
  text-align: center;
  padding: 10px;
}

.header a {
  color: #fff;
  padding-right: 5px;
  text-decoration: none;
}
</style>
