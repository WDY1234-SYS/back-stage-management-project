<template>
  <el-card class="box-card">
    <div slot="header" class="clearfix">
      <div class="header">
        <span>线上热门搜索</span>
        <el-dropdown>
          <span>
            <i class="el-icon-more"></i>
          </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>黄金糕</el-dropdown-item>
            <el-dropdown-item>狮子头</el-dropdown-item>
            <el-dropdown-item>螺蛳粉</el-dropdown-item>
            <el-dropdown-item>双皮奶</el-dropdown-item>
            <el-dropdown-item>蚵仔煎</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </div>
    </div>
    <el-row :gutter="10">
      <el-col :span="12">
        <LineCharts></LineCharts>
      </el-col>
      <el-col :span="12">
        <LineCharts></LineCharts>
      </el-col>
    </el-row>
    <!-- 表格 -->
    <el-table :data="tableData" style="width: 100%" border>
      <el-table-column label="排名" width="80px"> </el-table-column>
      <el-table-column label="搜索关键字" width="width"> </el-table-column>
      <el-table-column label="用户数" sortable width="width"> </el-table-column>
      <el-table-column label="周涨幅" sortable width="width"> </el-table-column>
    </el-table>
    <!-- 分页器 -->
    <el-pagination layout="prev, pager, next" :total="1000" class="pagination"> </el-pagination>
  </el-card>
</template>

<script>
import LineCharts from "./lineCharts";
export default {
  name: "",
  data() {
    return {
      tableData: [{}],
    };
  },
  components: {
    LineCharts,
  },
};
</script>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
}
.clearfix {
  border-bottom: 1px solid #eee;
  padding: 5px;
}
.pagination {
  float: right;
}
</style>