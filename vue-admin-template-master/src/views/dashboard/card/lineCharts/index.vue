<template>
  <!-- 容器 -->
  <div class="box" ref="charts"></div>
</template>

<script>
import echarts from "echarts";
export default {
  name: "",
  mounted() {
    let lineCharts = echarts.init(this.$refs.charts);
    lineCharts.setOption({
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
          type: "line",
          data: [10, 7, 33, 12, 48, 29, 10, 44],
          //拐点的样式设置
          itemStyle: {
            opacity: 0,
          },
          //线条的样式
          lineStyle: {
            color: "purple",
          },
          //填充颜色
          areaStyle: {
            color: {
              type: "linear",
              x: 0,
              y: 0,
              x2: 0,
              y2: 1,
              colorStops: [
                {
                  offset: 0,
                  color: "purple", // 0% 处的颜色
                },
                {
                  offset: 1,
                  color: "#fff", // 100% 处的颜色
                },
              ],
              global: false, // 缺省为 false
            },
          },
        },
      ],
      //布局调试
      grid: {
        left: 0,
        top: 0,
        right: 0,
        bottom: 0,
      },
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