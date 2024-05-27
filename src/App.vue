<template>
  <router-view v-if="isRouterAlive"></router-view>
</template>

<script setup>
import { onMounted, ref, nextTick, provide } from "vue";
// import city from "./mock/ningboCity";
import business from './business'
import { useStore } from "vuex";
// 局部组件刷新
const isRouterAlive = ref(true);
const globalStore = useStore();
const reload = () => {
  isRouterAlive.value = false;
  nextTick(() => {
    isRouterAlive.value = true;
    console.log("数据刷新成功");
  });
};
provide("reload", reload);
// 反转reset获得正序path
onMounted(() => {
  globalStore.dispatch("user/changeThem", "#4060c7");
  // console.log("city", city);
  console.log('business',business)
  const newBuss =[]
  business.forEach((element) => {
    const newCon = {
      name:element.name,
      center:element.center,
      path:[]
    }
    element.path.forEach((item) => {
      item = item.reverse()
      newCon.path.push(item)
      // item.forEach((ele) => {
      //   ele = ele.reverse()
      //   console.log('格式化后',ele)
      //   // ele.forEach((pr) => {
      //   //   console.log("ele ", pr);
      //   //   pr = pr.reverse();
      //   //   console.log("ele格式之后 ", pr);
      //   // });
      // });
    });
    newBuss.push(newCon)
  });
  console.log('newBuss',newBuss)
  // console.log("city", city);
});
</script>

<style scoped lang="scss"></style>
