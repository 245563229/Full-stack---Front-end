<template>
  <div id="echarts1"></div>
</template>
<script setup>
import * as echarts from "echarts";
import { onMounted } from "vue";

const creatEcharts = () => {
  let myChart = echarts.init(document.getElementById("echarts1"));
  // 指定图表的配置项和数据
  let option = {
    grid: {
      left: "28%",
      right: "20%",
      top: "0%",
      bottom: "0%",
      // width: 250,
    },
    xAxis: [
      {
        splitLine: {
          show: false,
        },
        type: "value",
        show: false,
      },
    ],
    yAxis: [
      {
        splitLine: {
          show: false,
        },
        axisLine: {
          //y轴
          show: false,
        },
        type: "category",
        axisTick: {
          show: false,
        },
        inverse: true,
        data: [
          "16-24岁",
          "25-30岁",
          "31-35岁",
          "36-40岁",
          "41-45岁",
          "46-50岁",
          "51-60岁",
          "61岁以上",
        ],
        axisLabel: {
          color: "#A7D6F4",
          fontSize: 14,
          margin: 20,
          formatter: function (value) {
            return value;
          },
        },
      },
      {
        type: "category",
        inverse: true,
        axisTick: "none",
        axisLine: "none",
        show: true,
        axisLabel: {
          textStyle: {
            color: "#A7D6F4",
            fontSize: "14",
          },
          formatter: function (value, index) {
            return `{a|${value}人}`;
          },
          rich: {
            a: {
              fontSize: 14,
              color: "rgba(34, 217, 246, 1)",
              padding: [4, 0, 0, 0],
            },
          },
        },
        // data: value,
        data: [900, 380, 360, 340, 320, 300, 280, 260],
      },
    ],
    series: [
      {
        name: "酒驾年龄排行",
        type: "bar",
        barWidth: 8, // 柱子宽度
        showBackground: true,
        MaxSize: 0,
        backgroundStyle: {
          color: "#0c3151",
        },
        label: {
          show: false,
          // color: '#A7D6F4',
          // fontSize: 14,
          // distance: 20, // 距离
          // formatter: '{c} ', // 这里是数据展示的时候显示的数据
          // align: "center",
          // position: [290, 0]
        }, // 柱子上方的数值
        itemStyle: {
          barBorderRadius: [0, 4, 4, 0], // 圆角（左上、右上、右下、左下）
          color: new echarts.graphic.LinearGradient(
            1,
            0,
            0,
            0,
            [
              {
                offset: 1,
                color: "rgba(34, 217, 246, 1)",
              },
              {
                offset: 0,
                color: "rgba(34, 149, 246, 1)",
              },
            ],
            false
          ), // 渐变
        },
        data: [900, 380, 360, 340, 320, 300, 280, 260],
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
