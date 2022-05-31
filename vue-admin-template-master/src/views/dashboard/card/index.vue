<template>
  <el-row :gutter="10">
    <el-col :span="6">
      <el-card>
        <Detail title="总销售额" count="￥156988">
            <template slot="charts">
                <span>周同比&nbsp;&nbsp;55.48%&nbsp;&nbsp;<svg t="1650113166787" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="2563" width="16" height="16"><path d="M960 704L512 256l-448 448z" fill="#1afa29" p-id="2564"></path></svg></span>               
                <span>日同比&nbsp;&nbsp;19.96%&nbsp;&nbsp;<svg t="1650113351617" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="3563" width="16" height="16"><path d="M64 320l448 448 448-448z" fill="#d81e06" p-id="3564"></path></svg></span>
            </template>
            <template slot="footer">
                <span>日销售额￥12564</span>
            </template>
        </Detail>
      </el-card>
    </el-col>
    <el-col :span="6">
      <el-card>
        <Detail title="访问量" count="46590">
            <template slot="charts">
               <LineCharts></LineCharts> 
            </template>
            <template slot="footer">
                <span>日访问量1564</span>
            </template>
        </Detail>
      </el-card>
    </el-col>
    <el-col :span="6">
      <el-card>
        <Detail title="支付笔数" count="15645">
            <template slot="charts">
               <BarCharts></BarCharts> 
            </template>
            <template slot="footer">
                <span>转换率64%</span>
            </template>
        </Detail>
      </el-card>
    </el-col>
    <el-col :span="6">
      <el-card>
        <Detail title="运营活动效果" count="78%">
            <template slot="charts">
               <ProgressCharts></ProgressCharts>
            </template>
            <template slot="footer">
                <span>周同比&nbsp;&nbsp;35.25%&nbsp;&nbsp;<svg t="1650113166787" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="2563" width="16" height="16"><path d="M960 704L512 256l-448 448z" fill="#1afa29" p-id="2564"></path></svg></span>               
                <span>日同比&nbsp;&nbsp;29.69%&nbsp;&nbsp;<svg t="1650113351617" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="3563" width="16" height="16"><path d="M64 320l448 448 448-448z" fill="#d81e06" p-id="3564"></path></svg></span>
            </template>
        </Detail>
      </el-card>
    </el-col>
  </el-row>
</template>

<script>
import Detail from "./detail";
import LineCharts from './lineCharts';
import BarCharts from './barCharts';
import ProgressCharts from './progressCharts'
export default {
  name: "Card",
  components: {
    Detail,
    LineCharts,
    BarCharts,
    ProgressCharts
  },
};
</script>

<style scoped>
span{
    margin-left:10px
}
</style>