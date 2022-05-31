<template>
  <div>
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <!-- v-model="activeName" @tab-click="handleClick" -->
        <!-- 头部左侧内容 -->
        <el-tabs class="tab" v-model="activeName">
          <el-tab-pane label="销售额" name="sale"></el-tab-pane>
          <el-tab-pane label="访问量" name="visits"></el-tab-pane>
        </el-tabs>
        <!-- 头部右侧内容 -->
        <div class="right">
          <span @click="setDay">今日</span>
          <span @click="setWeek">本周</span>
          <span @click="setMonth">本月</span>
          <span @click="setYear">本年</span>
          <el-date-picker
            v-model="date"
            class="date"
            type="daterange"
            range-separator="-"
            start-placeholder="开始日期"
            end-placeholder="结束日期"
            size="mini"
            value-format="yyyy-MM-dd"
          >
          </el-date-picker>
        </div>
      </div>
      <div>
        <el-row :gutter="10">
          <el-col :span="20">
            <BarCharts :title="title" :listState="listState"></BarCharts>
          </el-col>
          <el-col :span="4">
            <div class="bottom-right">
              <h3>门店{{ title }}排名</h3>
              <ul>
                <li>
                  <span class="rindex">1</span>
                  <span>肯德基</span>
                  <span class="rvalue">6663</span>
                </li>
                <li>
                  <span class="rindex">2</span>
                  <span>麦当劳</span>
                  <span class="rvalue">6688</span>
                </li>
                <li>
                  <span class="rindex">3</span>
                  <span>华莱士</span>
                  <span class="rvalue">34343434</span>
                </li>
                <li>
                  <span class="index">4</span>
                  <span>无敌小馒头</span>
                  <span class="rvalue">4334343</span>
                </li>
                <li>
                  <span class="index">5</span>
                  <span>星巴克</span>
                  <span class="rvalue">434378</span>
                </li>
                <li>
                  <span class="index">6</span>
                  <span>奶茶王</span>
                  <span class="rvalue">783783</span>
                </li>
                <li>
                  <span class="index">7</span>
                  <span>黄焖鸡</span>
                  <span class="rvalue">73373</span>
                </li>
              </ul>
            </div>
          </el-col>
        </el-row>
      </div>
    </el-card>
  </div>
</template>

<script>
import BarCharts from "./barCharts";
import dayjs from "dayjs";
import { mapState } from 'vuex';
export default {
  name: "",
  components: {
    BarCharts,
  },
  data() {
    return {
      activeName: "sale",
      //收集日历数据
      date: [],
    };
  },
  computed: {
    title() {
      return this.activeName == "sale" ? "销售额" : "访问量";
    },
    ...mapState({listState:state => state.home.list})
  },
  methods: {
    //本天
    setDay() {
      const day = dayjs().format("YYYY-MM-DD");
      this.date = [day, day];
    },
    //本周
    setWeek() {
      const start = dayjs().day(1).format("YYYY-MM-DD");
      const end = dayjs().day(7).format("YYYY-MM-DD");
      this.date = [start, end];
    },
    //本月
    setMonth() {
      const start = dayjs().startOf("month").format("YYYY-MM-DD");
      const end = dayjs().endOf("month").format("YYYY-MM-DD");
      this.date = [start, end];
    },
    //本年
    setYear() {
      const start = dayjs().startOf("year").format("YYYY-MM-DD");
      const end = dayjs().endOf("year").format("YYYY-MM-DD");
      this.date = [start, end];
    },
  },
};
</script>

<style scoped>
.box-card {
  margin: 10px 0;
}
.tab {
  width: 100%;
}
.clearfix {
  position: relative;
  display: flex;
  justify-content: space-between;
}
.right {
  position: absolute;
  right: 0;
}
.date {
  width: 250px;
  margin-left: 10px;
}
.right span {
  margin: auto 10px;
}
.bottom-right span {
  margin: auto 15px;
}
ul {
  list-style: none;
  width: 100%;
  height: 300px;
  padding: 0px;
}
ul li {
  height: 8%;
  margin: 10px 0px;
}
.rindex {
  float: left;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: black;
  color: white;
  text-align: center;
}
.rvalue {
  float: right;
}
.index {
  float: left;
  width: 20px;
  height: 20px;
  text-align: center;
}
h3 {
  font-weight: normal;
  font-size: 16px;
}
.right span {
    cursor: pointer;
}
.right span:hover {
    background-color: cyan;
}
</style>