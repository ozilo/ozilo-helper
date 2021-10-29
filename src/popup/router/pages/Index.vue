<template>
  <div
    id="tt"
    class="container">
  <div>
    <el-container>
      <el-header>
        <!--导航栏-->
        <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal" menu-trigger="click">
        <el-menu-item index="1">正在进行</el-menu-item>
        <el-submenu index="2">
          <template slot="title">工作台</template>
          <el-menu-item index="2-1">表格中心</el-menu-item>
          <el-menu-item index="2-2" @click="handleSelect">element文档中心</el-menu-item>
          <el-menu-item index="2-3">item three</el-menu-item>
          <el-submenu index="2-4">
            <template slot="title">item four</template>
            <el-menu-item index="2-4-1">item one</el-menu-item>
            <el-menu-item index="2-4-2">item two</el-menu-item>
            <el-menu-item index="2-4-3">item three</el-menu-item>
          </el-submenu>
        </el-submenu>
        <el-menu-item index="3" disabled>Info</el-menu-item>
        <el-menu-item index="4"><a href="https://www.google.com" target="_blank">Google</a></el-menu-item>
        </el-menu>
      </el-header>
      <el-main>
        <el-table
          :data="tableData">
        <el-table-column
          prop="date"
          label="Date"
          width="180">
        </el-table-column>
        <el-table-column
          prop="name"
          label="Name"
          width="180">
        </el-table-column>
        <el-table-column
          prop="address"
          label="Address">
        </el-table-column>
        </el-table>
      </el-main>
      <el-footer class='m-footer'>
      <!--搜索键-->
      <el-button type="primary" icon="el-icon-search" @click="webSearch">Search</el-button>
      </el-footer>
    </el-container>
  </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeIndex: '1',
      tableData: [],
    };
  },
  methods: {
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
      chrome.tabs.create({ url: "https://element.eleme.cn/#/zh-CN"});
    },
    webSearch() {
      chrome.tabs.create({ url: "http://google.com" });
    },
    getTableData(){
      this.$axios.post('/api/selectDemoTableData').then((res) => {
        this.tableData = res.data;
      }).catch(function(error){
        console.log(error);
      })
    }
  },
  option() {
    chrome.tabs.create({ url: "http://google.com" });
  },
};
</script>

<style lang="scss" scoped>
.container {
  min-width: 600px;
  min-height: 150px;
  max-height: 800px;
  overflow-y: auto;
  padding: 10px 7px;
  box-sizing: border-box;
  position: relative;
  font-size: 12px;
  font-family: "Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB",
    "Microsoft YaHei", "微软雅黑", Arial, sans-serif;
}
.el-container{
  position: relative;
  width: 100%;
  height: 400px;
  bottom: 1px;
}
.el-header {
  position: relative;
  box-sizing: border-box;
  width: 100%;
  height: 60px;
}
.el-footer {
  position: relative;
  box-sizing: border-box;
  width: 100%;
  height: 30px;
  bottom: 0;
  line-height: 30px;
}
 .m-footer {
    height: 30px !important;
  }
.el-main {
  position: relative;
  left: 1px;
  right: 1px;
  top: 1px;
  bottom: 0;
  overflow-y: scroll;
}
</style>
