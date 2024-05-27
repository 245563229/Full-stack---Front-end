<template>
  <el-input v-model="num" placeholder="请输入带有后缀的文件名" />
  <el-button type="primary" @click="changeNum">删除指定元素</el-button>
</template>

<script setup>
import { onMounted, reactive, ref } from "vue";

const num = ref();

const changeNum = () => {
  if (num.value) {
    num.value = num.value.substring(num.value.lastIndexOf(".") + 1);
  }
};
</script>

<style scoped lang="scss"></style>
