<template>
  <el-container style="height: 100%" v-loading="loading">
    <el-aside width="400px"> </el-aside>
    <el-main>
      <iframe src="/static/sp.html?codeId=002266" class="myIframe"></iframe>
    </el-main>
  </el-container>
</template>

</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      loading:false,
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 
.myIframe {
  width: 100%;
  height: 100%;
}
.el-main {
  margin: 0px;
  padding: 0px;
}
</style>
