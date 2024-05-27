<template>
  <el-table :data="tableData" style="width: 100%">
    <el-table-column prop="name" label="Name" width="180" />
    <el-table-column prop="status" label="状态">
      <template #default="scoped">
        <statusDot :color="colorSelect(scoped.row.status).color" size="10px">{{
          scoped.row.status
        }}</statusDot>
      </template>
    </el-table-column>
  </el-table>
</template>
<script setup>
import { reactive, ref } from "vue";
import statusDot from "./statusDot.vue";
const tableData = ref([
  {
    name: "状态1",
    status: "1",
  },
  {
    name: "状态2",
    status: "2",
  },
  {
    name: "状态3",
    status: "3",
  },
  {
    name: "状态4",
    status: "4",
  },
]);
const state = reactive({
  StatusColor: [
    { status: "0", color: "#faad14" },
    { status: "1", color: "#1890ff" },
    { status: "2", color: "#52c41a" },
    { status: "3", color: "#f5222d" },
    { status: "4", color: "#7546c9" },
  ],
});
//筛选符合项
const colorSelect = (status) => {
  return state.StatusColor.find((item) => {
    return item.status == status;
  });
};
</script>
<style scoped lang="scss"></style>
