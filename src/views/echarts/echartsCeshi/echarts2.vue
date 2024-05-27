<template>
  <div id="echarts2"></div>
</template>
<script setup>
import * as echarts from "echarts";
import { onMounted } from "vue";

const creatEcharts = () => {
  let myChart = echarts.init(document.getElementById("echarts2"));
  var data = [2250, 1960, 1270, 1020];
  var className = ["2020年", "2021年", "2022年", "2023年"];
  var defaultData = [3000, 3000, 3000, 3000];
  // 指定图表的配置项和数据
  let option = {
    // backgroundColor: "#002D54",
    grid: {
      left: "3%",
      right: "20%",
      top: "4%",
      bottom: `${95 - defaultData.length * 15}%`,
      // width: 250,
    },
    xAxis: {
      type: "value",
      splitLine: {
        show: false,
      },
      axisTick: {
        show: false,
      },
      axisLabel: {
        //  改变x轴字体颜色和大小
        show: false,
      },
    },
    yAxis: [
      {
        type: "category",
        inverse: true,
        axisLabel: {
          show: true,
          margin: 2,

          textStyle: {
            color: "#fff",
            fontSize: "14",
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
        data: className,
      },
      {
        type: "category",
        inverse: true,
        axisTick: "none",
        axisLine: "none",
        show: true,
        axisLabel: {
          textStyle: {
            color: "rgba(34, 217, 246, 1)",
            fontSize: "14",
          },

          formatter: function (value) {
            return " " + value + "人";
          },
        },
        data: data,
      },
    ],
    series: [
      {
        name: "酒驾时间排行",
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
                  color: "rgba(3, 42, 47, 0.5)",
                },
                {
                  offset: 0,
                  color: "rgba(16, 182, 236, 1)",
                },
              ],
              false
            ),
          },
        },
        barWidth: 12,
        data: data,
      },
      {
        name: "背景",
        type: "bar",
        barWidth: 12,
        barGap: "-100%",
        data: defaultData,
        itemStyle: {
          normal: {
            color: "rgba(3, 42, 47, 1)",
            barBorderRadius: 0,
          },
        },
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
