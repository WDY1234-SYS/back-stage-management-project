<template>
  <div class="box" ref="bar"></div>
</template>

<script>
import echarts from "echarts";
export default {
  name: "",
  data() {
    return {
      barCharts: null,
    };
  },
  props: ['title', 'listState'],
  mounted() {
    this.barCharts = echarts.init(this.$refs.bar);
    this.barCharts.setOption({
      title: {
        text: this.title + '趋势'
      },
      tooltip: {
        trigger: "axis",
        axisPointer: {
          type: "shadow",
        },
      },
      grid: {
        left: "3%",
        right: "4%",
        bottom: "3%",
        containLabel: true,
      },
      xAxis: [
        {
          type: "category",
          data: [],
          axisTick: {
            alignWithLabel: true,
          },
        },
      ],
      yAxis: [
        {
          type: "value",
        },
      ],
      series: [
        {
          name: "Direct",
          type: "bar",
          barWidth: "60%",
          data: [],
          color: 'yellowgreen'
        },
      ],
    });
  },
  //监听属性
  watch: {
    title() {
      //重新修改图表配置的数据
      this.barCharts.setOption({
        title: {
          text: this.title + '趋势'
        },
        xAxis: {
          data: this.title == '销售额' ? this.listState.orderFullYearAxis : this.listState.userFullYearAxis
        },
        series: {
          name: 'Direct',
          type: 'bar',
          barWidth: '60%',
          data: this.title == '销售额' ? this.listState.orderFullYear : this.listState.userFullYear,
          color: 'yellowgreen'
        }
      })
    },
    listState() {
      this.barCharts.setOption({
        title: {
          text: this.title + '趋势'
        },
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "shadow",
          },
        },
        grid: {
          left: "3%",
          right: "4%",
          bottom: "3%",
          containLabel: true,
        },
        xAxis: [
          {
            type: "category",
            data: this.listState.orderFullYearAxis,
            axisTick: {
              alignWithLabel: true,
            },
          },
        ],
        yAxis: [
          {
            type: "value",
          },
        ],
        series: [
          {
            name: "Direct",
            type: "bar",
            barWidth: "60%",
            data: this.listState.orderFullYear,
            color: 'yellowgreen'
          },
        ],
      });
    }
  }
};
</script>

<style scoped>
.box {
  width: 100%;
  height: 300px;
}
</style>