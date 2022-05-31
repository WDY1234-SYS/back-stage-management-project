<template>
  <!-- 容器 -->
  <div class="box" ref="charts"></div>
</template>

<script>
import echarts from "echarts";
export default {
  name: "",
  mounted() {
    let barCharts = echarts.init(this.$refs.charts);
    barCharts.setOption({
      xAxis: {
        //隐藏x轴
        show: false,
        //
        type: "category",
      },
      yAxis: {
        show: false,
      },
      //系列
      series: [
        {
          type: "bar",
          data: [10, 7, 33, 12, 48, 29, 10, 44,20,50,42,56],
          color:'blue'
        },
      ],
      //布局调试
      grid: {
        left: 0,
        top: 0,
        right: 0,
        bottom: 0,
      },
      //提示组件
      tooltip:{}
    });
  },
};
</script>

<style>
.box {
  width: 100%;
  height: 100%;
}
</style>