<template>
<el-input v-model="state.val"></el-input>
  <div>
    {{ priceFor(state.val) }}
  </div>
</template>
<script setup>
import { reactive, ref } from "vue";
import statusDot from "./statusDot.vue";

const state = reactive({
val:''
});
//转为金额格式
const priceFor = (val)=> {
  if(!val){
    return ''
  }else if(val.length<4){
    return val
  }else {
    let str = val+''
    let numList = []
    for(let i = 1;i<=str.length;i=i+0){
      if(str.length>=4){
        numList.unshift(str.substring(str.length - 3, str.length))
        str = str.slice(0, -3)
      }else {
        numList.unshift(str)
        str = ''
      }
    }
    return numList.join(',')
  }
}

</script>
<style scoped lang="scss"></style>
