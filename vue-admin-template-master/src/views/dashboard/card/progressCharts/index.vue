<template>
  <!-- 容器 -->
  <div class="box" ref="charts"></div>
</template>

<script>
import echarts from "echarts";
export default {
  name: "",
  mounted() {
    let progressCharts = echarts.init(this.$refs.charts);
    progressCharts.setOption({
      xAxis: {
        //隐藏x轴
        show: false,
        //最小值和最大值
        min: 0,
        max: 100,
      },
      yAxis: {
        show: false,
        type: "category",
      },
      //系列
      series: [
        {
          type: "bar",
          data: [78],
          color: "yellowgreen",
          //柱状图宽度
          barWidth: "20%",
          //背景颜色设置
          showBackground: true,
          backgroundStyle: {
              color:'#eee'
          },
          //文本标签
          label:{
              show:true,
              //改变文本内容
              formatter:'|',
              //文本标签位置
              position:'right'
          }
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
      tooltip: {},
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