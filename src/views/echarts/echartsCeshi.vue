<template>
  <div class="dialogClass" v-if="showList">
    <div class="echartsClass">
      <div class="echartsTitleClass">
        <div class="imageClass"></div>
        酒驾年龄排行
      </div>
      <echarts1 class="echartsAllClass"></echarts1>
    </div>
    <div class="drelineClass" />
    <div class="echartsClass">
      <div class="echartsTitleClass">
        <div class="imageClass"></div>
        酒驾年龄排行
      </div>
      <echarts2 class="echartsAllClass"></echarts2>
    </div>
    <div class="drelineClass" />
    <div class="echartsClass">
      <div class="echartsTitleClass">
        <div class="imageClass"></div>
        酒驾车辆排行
      </div>

      <echarts3 class="echartsAllClass"></echarts3>
    </div>
    <div class="drelineClass" />

    <div class="echartsClass">
      <div class="echartsTitleClass">
        <div class="imageClass"></div>
        酒驾事故排行
      </div>
      <echarts4 class="echartsAllClass"> </echarts4>
    </div>
    <div class="cancelClass" @click="showList = false"></div>
  </div>
  <!-- <div>
    <echarts5></echarts5>
  </div> -->
  <!-- <div>
    <echarts6></echarts6>
  </div> -->
</template>
<script setup>
import { ref, defineEmits } from "vue";
import echarts1 from "./echartsCeshi/echarts1.vue";
import echarts2 from "./echartsCeshi/echarts2.vue";
import echarts3 from "./echartsCeshi/echarts3.vue";
import echarts4 from "./echartsCeshi/echarts4.vue";
import echarts5 from "./echartsCeshi/echarts5.vue";
import echarts6 from "./echartsCeshi/echarts6.vue";
const showList = ref(false);
</script>
<style scoped lang="scss">
.dialogClass {
  position: absolute;
  top: calc(50% - 220px);
  left: calc(50% - 650px);
  width: 1300px;
  height: 440px;
  background: url(../../assets/images/diaBG.png);
  background-size: 100% 100%;
  background-repeat: no-repeat;
  display: flex;
  padding: 50px 30px 20px 30px;
  // > div {
  //   margin-right: 20px;
  // }
  .cancelClass {
    right: 30px;
    top: 30px;
    position: absolute;
    width: 18px;
    height: 18px;
    background: url(../../assets/images/dialogCancel.png);
    background-size: 100% 100%;
    background-repeat: no-repeat;
    cursor: pointer;
  }
}
.echartsClass {
  flex: 1;
}
.echartsAllClass {
  width: calc(100%);
  height: calc(100% - 50px);
}
.echartsTitleClass {
  display: flex;
  justify-content: left;
  padding-left: 10px;
  height: 50px;
  font-size: 18px;
  font-family: Source Han Sans CN;
  font-weight: 400;
  color: #ffffff;
}
.imageClass {
  margin-right: 5px;
  width: 20px;
  height: 8px;
  background: url(../../assets/images/diologTitleBG.png);
  background-size: 100% 100%;
  background-repeat: no-repeat;
}
.drelineClass {
  float: left;
  width: 1px;
  margin-top: 80px;
  height: 75%;
  margin-left: 20px;
  margin-right: 20px;
  // margin-left: 3.5em;
  background: radial-gradient(
    circle at 50% 50%,
    rgba(255, 255, 255, 1),
    rgba(255, 255, 255, 0)
  );
}
</style>
