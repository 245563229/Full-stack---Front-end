<template>
  <div id="echarts4"></div>
</template>
<script setup>
import * as echarts from "echarts";
import { onMounted } from "vue";

const creatEcharts = () => {
  let salvProName = ["未伤人事故数量", "伤人事故数量", "致死事故数量"];
  let data = [42850, 18520, 3250];
  let dataBg = [1, 1, 1, 1];
  let maxData = 50000;
  let myChart = echarts.init(document.getElementById("echarts4"));
  // 指定图表的配置项和数据
  let option = {
    // backgroundColor: "#000",
    grid: {
      left: "3%",
      right: "25%",
      top: "4%",
      bottom: `${99 - data.length * 15}%`,
      // containLabel: true
    },
    xAxis: [
      {
        type: "value",
        max: maxData,
        show: false,
      },
      {
        type: "value",
        show: false,
      },
    ],

    yAxis: [
      {
        type: "category",
        inverse: true,
        axisLabel: {
          show: true,
          margin: 2,
          textStyle: {
            color: "#fff",
            fontSize: 14,
          },
          // 调整左侧文字的3个属性，缺一不可
          verticalAlign: "bottom",
          align: "top",
          //调整文字上右下左
          padding: [15, 0, 15, 0],
        },
        splitLine: {
          show: false,
        },
        axisTick: {
          show: false,
        },
        axisLine: {
          show: false,
        },
        data: salvProName,
      },
      {
        type: "category",
        inverse: true,
        axisTick: "none",
        axisLine: "none",
        show: true,
        axisLabel: {
          textStyle: {
            color: "rgba(207, 172, 37, 1)",
            fontSize: "14",
          },
          formatter: function (value) {
            return "  " + value + "起";
          },
        },
        data: data,
      },
    ],
    series: [
      {
        name: "酒驾事故排行",
        type: "bar",
        zlevel: 1,
        itemStyle: {
          normal: {
            barBorderRadius: 0,
            color: new echarts.graphic.LinearGradient(
              1,
              0,
              0,
              0,
              [
                {
                  offset: 1,
                  color: "rgba(3, 42, 47, 1)",
                },
                {
                  offset: 0,
                  color: "rgba(196, 179, 39, 1)",
                },
              ],
              false
            ),
          },
        },
        barWidth: 8,
        barGap: "0%",

        data: data,
      },
      {
        name: "背景部分",
        type: "bar",
        xAxisIndex: 1,
        barWidth: 8,
        barGap: "-100%",
        data: dataBg,
        itemStyle: {
          normal: {
            color: "#D0DEEE",
            opacity: 0.1,
          },
        },
      },
      // 进度条的小圆圈
      {
        name: "小圈圈",
        type: "scatter",
        emphasis: {
          scale: false,
        },
        symbol:
          "image://data:image/png;base64,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",
        symbolSize: [24, 24],
        itemStyle: {
          color: "#FFF",
          shadowColor: "rgba(255, 255, 255, 1)",
          shadowBlur: 2,
          borderWidth: 1,
          opacity: 1,
        },
        z: 2,
        zlevel: 10,
        data: data,
        animationDelay: 500,
      },
    ],
    // dataZoom: [
    //   {
    //     yAxisIndex: [0, 1], // 这里是从X轴的0刻度开始
    //     show: false, // 是否显示滑动条，不影响使用
    //     type: "slider", // 这个 dataZoom 组件是 slider 型 dataZoom 组件
    //     startValue: 0, // 从头开始。
    //     endValue: 5, // 展示到第几个。
    //   },
    // ],
  };
  myChart.setOption(option);
};

// 使用刚指定的配置项和数据显示图表。
onMounted(() => {
  creatEcharts();
});
</script>
<style scoped lang="scss"></style>
