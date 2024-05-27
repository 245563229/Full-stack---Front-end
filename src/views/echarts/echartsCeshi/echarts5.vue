<template>
  <div id="echarts5" style="width: 800px; height: 400px"></div>
</template>
<script setup>
import * as echarts from "echarts";
import { onMounted } from "vue";

const creatEcharts = () => {
  let max = 400;
  let value = [200];
  let myChart = echarts.init(document.getElementById("echarts5"));
  // 指定图表的配置项和数据
  let option = {
    backgroundColor: "#000A2A", //背景必须与symbal颜色一样
    grid: {
      left: "20%",
      right: "20%",
    },
    xAxis: {
      type: "value",
      max: max,
      splitLine: {
        show: false,
      },
      axisLine: {
        show: false,
      },
      axisLabel: {
        show: false,
      },
      axisTick: {
        show: false,
      },
    },
    yAxis: [
      {
        type: "category",
        inverse: true,
        data: ["一产"],
        axisLine: {
          show: false,
        },
        axisTick: {
          show: false,
        },
        axisLabel: {
          margin: 10,
          textStyle: {
            color: "#fff",
            fontSize: 40,
          },
        },
      },
      {
        type: "category",
        inverse: true,
        data: ["40%"],
        axisLine: {
          show: false,
        },
        axisTick: {
          show: false,
        },
        axisLabel: {
          margin: 10,
          textStyle: {
            color: "#00F0FF",
            fontSize: 60,
          },
        },
      },
    ],
    series: [
      {
        //内
        type: "bar",
        barWidth: 40,
        legendHoverLink: false,
        silent: true,
        position: "insideRight",
        itemStyle: {
          color: {
            type: "linear",
            x: 0,
            y: 0,
            x2: 1,
            y2: 0,
            colorStops: [
              {
                offset: 0,
                color: "#0078FF", // 0% 处的颜色
              },
              {
                offset: 1,
                color: "#00DEFF", // 100% 处的颜色
              },
            ],
            globalCoord: false, // 缺省为 false
          }, //底色
        },
        data: [200],
      },
      {
        //内
        type: "bar",
        barWidth: 40,
        legendHoverLink: false,
        silent: true,
        itemStyle: {
          color: {
            type: "linear",
            x: 0,
            y: 0,
            x2: 1,
            y2: 0,
            colorStops: [
              {
                offset: 0,
                color: "rgba(2, 38, 43, 1)", // 0% 处的颜色
              },
              {
                offset: 1,
                color: "rgba(232, 183, 34, 1)", // 100% 处的颜色
              },
            ],
            globalCoord: false, // 缺省为 false
          }, //底色
        },
        data: [200],
      },
      {
        //框
        type: "bar",
        barWidth: 50,
        barGap: "-110%",
        label: {
          normal: {
            show: false,
            position: "right",
            textStyle: {
              color: "#000",
            },
          },
        },
        itemStyle: {
          normal: {
            color: "rgba(0,0,0,0)", //底色
            borderWidth: 2,
            borderColor: "#004E77",
          },
        },
        data: [400],
        z: 1,
      },
      {
        //分隔
        type: "pictorialBar",
        itemStyle: {
          color: "#000A2A",
        },
        symbolRepeat: "fixed",
        symbolMargin: "20",
        symbol: "rect",
        symbolClip: true,
        symbolSize: [4, 48],
        symbolPosition: "start",
        symbolOffset: [0, 0],
        symbolBoundingData: max,
        data: [200],
        z: 5,
      },
      {
        //分隔
        type: "pictorialBar",
        itemStyle: {
          color: "#000A2A",
        },
        symbolRepeat: "fixed",
        symbolMargin: "20",
        symbol: "rect",
        symbolClip: true,
        symbolSize: [4, 48],
        symbolPosition: "start",
        symbolOffset: [0, 0],
        symbolBoundingData: max,
        data: [200],
        z: 5,
      },
    ],
  };
  myChart.setOption(option);
};

// 使用刚指定的配置项和数据显示图表。
onMounted(() => {
  creatEcharts();
});
</script>
<style scoped lang="scss"></style>
