<template>
  <div id="echarts6" style="width: 800px; height: 400px"></div>
</template>
<script setup>
import * as echarts from "echarts";
import { onMounted } from "vue";
// {
// 			name: "外圆",
// 			type: "scatter",
// 			emphasis: {
// 				scale: false,
// 			},
// 			symbol: "rect",
// 			symbolSize: [5,16],
// 			itemStyle: {
// 				color: '#FFF',
// 				shadowColor: "rgba(255, 255, 255, 0.5)",
// 				shadowBlur: 5,
// 				borderWidth: 1,
// 				opacity: 1,
// 			},
// 			z: 2,
// 			data: result,
// 			animationDelay: 500,
// 		},
const creatEcharts = () => {
  let myChart = echarts.init(document.getElementById("echarts6"));
  // 指定图表的配置项和数据
  let option = {
    backgroundColor: "#000",
    grid: {
      containLabel: true,
      bottom: "40%", //此处实际使用修改；我这里方便预览
      left: "10%", //此处实际使用修改；我这里方便预览
      top: "40%", //此处实际使用修改；我这里方便预览
      right: "10%", //此处实际使用修改；我这里方便预览
    },
    xAxis: {
      type: "value",
      axisLabel: {
        // color: '#b9bdc9',
        // fontSize: '12px',
        show: false,
      },
      axisLine: {
        show: false,
      },
      axisTick: {
        show: false,
      },
      splitLine: {
        show: false,
      },
    },
    yAxis: [
      {
        type: "category",
        data: ["法人一件事"],
        inverse: true,
        axisLabel: {
          fontSize: "17px",
          color: "#fff",
          inside: false, //是否内部
          margin: 10, //刻度标签与轴线之间的距离
        },
        axisLine: {
          show: false,
        },
        axisTick: {
          show: false,
        },
        splitLine: {
          show: false,
          lineStyle: {
            color: "#13387a",
          },
        },
      },
    ],
    color: ["#2DF3EC", "#1AA4F3"],
    series: [
      {
        name: "常住人口",
        type: "bar",
        stack: "total",
        label: {
          show: true,
          position: "insideLeft",
          distance: 2,
          formatter: (val) => {
            return `{a|${val.data}%}\n\n{a|}`;
          },
          rich: {
            a: {
              height: 20,
              lineHeight: 20,
              fontSize: 20,
              fontWeight: 600,
              color: "#2FFEF2",
            },
          },
        },
        // emphasis: {
        //    focus: 'series',
        //    disabled: true
        // },
        barWidth: 11,
        data: [50],
      },
      {
        name: "即办件占比",
        type: "bar",
        stack: "total",
        label: {
          show: true,
          // 想让显示在柱子的内部右侧 (左右位置)
          // 上下位置默认是居中的
          position: "insideRight",
          distance: 2,
          formatter: (val) => {
            // 通过\n换行加一倍的高度和换行让其显示在上方
            return `{a|${val.data}%}\n\n{a|}`;
          },
          rich: {
            a: {
              height: 20,
              lineHeight: 20,
              fontSize: 20,
              fontWeight: 600,
              color: "#239EEF",
            },
          },
        },
        // emphasis: {
        //    focus: 'series',
        //    disabled: true
        // },
        barWidth: 11,
        data: [50],
      },
      // {
      //   //分隔
      //   type: "pictorialBar",
      //   itemStyle: {
      //     color: "#000A2A",
      //   },
      //   symbolRepeat: "fixed",
      //   symbolMargin: "4",
      //   symbol: "rect",
      //   symbolClip: true,
      //   symbolSize: [2, 11],
      //   symbolPosition: "start",
      //   symbolOffset: [0, 0],
      //   symbolBoundingData: 100,
      //   data: [50],
      //   z: 5,
      // },
      {
        //分隔
        type: "pictorialBar",
        itemStyle: {
          color: "#000A2A",
        },
        symbolRepeat: "fixed",
        symbolMargin: "4",
        symbol: "rect",
        symbolClip: true,
        symbolSize: [2, 11],
        symbolPosition: "start",
        symbolOffset: [0, 0],
        symbolBoundingData: 100,
        data: [100],
        z: 5,
      },
      // {
      //   //分隔
      //   type: "pictorialBar",
      //   itemStyle: {
      //     color: "#000A2A",
      //   },
      //   symbolRepeat: "fixed",
      //   symbolMargin: "4",
      //   symbol: "rect",
      //   symbolClip: true,
      //   symbolSize: [2, 11],
      //   symbolPosition: "start",
      //   symbolOffset: [10, 0],
      //   symbolBoundingData: 100,
      //   data: [10],
      //   z: 5,
      // },
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
