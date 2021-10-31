<template>
  <el-container style="height: 100%" v-loading="loading">
    <el-main>
      <iframe :src="iframeUrl" class="myIframe"></iframe>
    </el-main>
    <el-aside width="340px">
      <avue-form
        ref="form"
        v-model="obj"
        :option="formOption"
        @reset-change="emptytChange"
        @submit="submit"
      >
      </avue-form>
      <avue-crud :option="option" :data="data" class="grid">
        <template slot="symbol" slot-scope="scope">
          <span class="crud-cell-blue" @click="lookAt(scope.row)">{{
            scope.row.symbol
          }}</span>
        </template>
      </avue-crud>
    </el-aside>
  </el-container>
</template>
<script>
var DIC = {
  VAILD: [
    {
      label: "否",
      value: "0",
    },
    {
      label: "是",
      value: "1",
    },
  ],
};
export default {
  name: "HelloWorld",
  data() {
    return {
      obj: { codeId: "", name: "", industry: "", isMy: "0", qzq: "0" , zc:'0' },
      Industry: [],
      data: [],
      iframeUrl: "",
      option: {
        menuType: "button",
        menuBtnTitle: "操作",
        dateBtn: false,
        dateDefault: false,
        border: true,
        menu: false,
        index: true,
        indexLabel: "序号",
        stripe: false,
        selection: false,
        menuAlign: "center",
        align: "center",
        addBtn: false,
        editBtn: false,
        delBtn: false,
        viewBtn: false,
        searchBtn: false,
        searchShow: false,
        calcHeight: 10,
        size: "mini",
        stripe: true,
        searchMenuSpan: 3,
        columnBtn: false,
        refreshBtn: false,
        menuWidth: 60,
        column: [
          {
            label: "代码",
            prop: "symbol",
            sortable: true,
            width: "80px",
          },
          {
            label: "名称",
            prop: "name",
            sortable: true,
            searchSpan: 12,
          },
          {
            label: "行业",
            prop: "industry",
            sortable: true,
            searchSpan: 12,
          },
        ],
      },
      loading: true,
    };
  },
  computed: {
    formOption() {
      var fo = {
        size: "mini",
        mockBtn: false,
        submitBtn: true,
        printBtn: false,
        column: [
          {
            label: "代码",
            prop: "codeId",
            row: true,
            span: 24,
            enter: this.getData,
          },
          {
            label: "名称",
            prop: "name",
            row: true,
            span: 24,
            enter: this.getData,
          },
          {
            label: "行业",
            type: "select",
            filterable: true,
            prop: "industry",
            dicData: this.Industry,
            size: "mini",
            row: true,
            span: 24,
            enter: this.getData,
          },
          {
            label: "自选",
            prop: "isMy",
            span: 24,
            type: "switch",
            dicData: DIC.VAILD,
            mock: {
              type: "dic",
            },
            row: true,
            enter: this.getData,
          }, {
            label: "强中强",
            prop: "qzq",
            span: 24,
            type: "switch",
            dicData: DIC.VAILD,
            mock: {
              type: "dic",
            },
            row: true,
            enter: this.getData,
          }, {
            label: "支撑",
            prop: "zc",
            span: 24,
            type: "switch",
            dicData: DIC.VAILD,
            mock: {
              type: "dic",
            },
            row: true,
            enter: this.getData,
          }
        ],
      };
      return fo;
    },
  },
  methods: {
    lookAt(row) {
      this.iframeUrl = `/static/sp.html?codeId=${row.symbol}&order=${
        row.$index + 1
      }`;
    },
    emptytChange() {
      this.getData();
    },
    submit(param, done) {
      this.getData();
      done();
    },
    getData(isInit) {
      this.loading = true;
      const api = `/sp/getbasic?codeId=${this.obj.codeId}&name=${this.obj.name}&industry=${this.obj.industry}&isMy=${this.obj.isMy}&qzq=${this.obj.qzq}&zc=${this.obj.zc}`;
      this.axios.get(api).then((response) => {
        this.loading = false;
        this.data = response.data;
        if (isInit) {
          this.Industry = [];
          let temp = {};
          for (let i = 0; i < this.data.length; i++) {
            let val = this.data[i].industry;
            if (!temp.hasOwnProperty(val)) {
              temp[val] = val;
            }
          }
          for (let prop in temp) {
            this.Industry.push({
              label: prop,
              value: prop,
            });
          }
          temp = null;
        }
      });
    },
  },
  mounted() {
    this.obj.qzq = "1";
    this.obj.isMy = "1";
    this.getData(true);
  },
};
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
.crud-cell-blue {
  color: red !important;
}
.grid {
  overflow-x: hidden;
}
</style>
