<template>
  <div>
    <div class="header">
      <span class="search-header">搜索用户数</span>
      <svg
        t="1650111775080"
        class="icon"
        viewBox="0 0 1024 1024"
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        p-id="2854"
        width="32"
        height="32"
      >
        <path
          d="M509.92 795.84c157.904 0 285.92-128.016 285.92-285.92C795.84 352 667.808 224 509.92 224 352 224 224 352 224 509.92c0 157.904 128 285.92 285.92 285.92z m0 48C325.504 843.84 176 694.32 176 509.92 176 325.504 325.504 176 509.92 176c184.416 0 333.92 149.504 333.92 333.92 0 184.416-149.504 333.92-333.92 333.92z m-2.448-400.704h16a16 16 0 0 1 16 16v201.728a16 16 0 0 1-16 16h-16a16 16 0 0 1-16-16V459.136a16 16 0 0 1 16-16z m0-100.176h16a16 16 0 0 1 16 16v23.648a16 16 0 0 1-16 16h-16a16 16 0 0 1-16-16v-23.648a16 16 0 0 1 16-16z"
          p-id="2855"
          fill="#d9d9d9"
        ></path>
      </svg>
    </div>
    <div class="main">
      <span class="main-left">12321</span>
      <span class="main-right">17.1</span>
      <!-- 向上图标 -->
      <svg
        t="1650113166787"
        class="icon"
        viewBox="0 0 1024 1024"
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        p-id="2563"
        width="16"
        height="16"
      >
        <path d="M960 704L512 256l-448 448z" fill="#1afa29" p-id="2564"></path>
      </svg>
      <!-- 向下图标 -->
      <svg
        t="1650113351617"
        class="icon"
        viewBox="0 0 1024 1024"
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        p-id="3563"
        width="16"
        height="16"
      >
        <path d="M64 320l448 448 448-448z" fill="#d81e06" p-id="3564"></path>
      </svg>
      <!-- 容器 -->
      <div class="line" ref="charts"></div>
    </div>
    <div class="footer">
      
    </div>
  </div>
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
            color: "skyblue",
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
                  color: "skyblue", // 0% 处的颜色
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

<style scoped>
.header {
  display: flex;
  align-items: center;
}
.search-header {
  margin-right: 20px;
}
.main-left {
  margin-right: 30px;
  font-size: 20px;
}
.main-right {
  margin-right: 10px;
}
.line {
  width: 100%;
  height: 50px;
}
</style>