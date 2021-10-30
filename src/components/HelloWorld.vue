<template>
  <el-container style="height: 100%" v-loading="loading">
  
    <el-main>
      <iframe :src="iframeUrl" class="myIframe"></iframe>
    </el-main>
      <el-aside width="300px"> 
      <avue-crud :option="option" :data="data">
          <template slot="symbol" slot-scope="scope">
              <span class="crud-cell-blue" @click="lookAt(scope.row)">{{scope.row.symbol}}</span>
          </template>
         <!-- <template slot="menu" slot-scope="scope">
              <el-button size="small" type="text"  @click.native="lookAt(scope.row)">查看</el-button>
          </template> -->
      </avue-crud>
    </el-aside>
  </el-container>
  
</template>
<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
     data:[],
     iframeUrl:'',
     option:{
          menuType:'button',
          menuBtnTitle:'操作',
          dateBtn:false,
          dateDefault:false,
          border: true,
          menu: false,//菜單顯示
          index: false,
          indexLabel: '序号',
          stripe: false,
          selection: false,
          menuAlign: 'center',
          align: 'center',
          addBtn: false,
          editBtn:false,
          delBtn:false,
          viewBtn: false,
          searchBtn: false,
          searchShow: false,
          calcHeight: 10,
          searchMenuSpan: 3,
          menuWidth:60,
          // searchMenuPosition:'right',
          column: [{
            label: '代码',
            prop: 'symbol',                        
            sortable:true,
            width:'80px',          
          },{
            label: '名称',
            prop: 'name',
            sortable:true,
            searchSpan:12, 
          },{
            label: '行业',
            prop: 'industry',
            sortable:true,
            searchSpan:12, 
          }]
      },
      loading:true, 
    }
  },
  methods: {
      lookAt(row){
          this.iframeUrl = '/static/sp.html?codeId='+ row.symbol
      },
  },
  mounted(){
     const api = `/sp/getbasic/`
     this.axios.get(api).then((response) => {
       this.loading = false       
       this.data = response.data
    })
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
  overflow: hidden;
}
.crud-cell-blue{
  color:red !important;
}
</style>
