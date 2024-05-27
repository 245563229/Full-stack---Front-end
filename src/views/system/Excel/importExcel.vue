<template>
  <el-card>
    <el-button type="primary" @click="importExcel">导入Excel</el-button>
  </el-card>
  <filesUpload ref="importRef" @gatewayData="gatewayData"></filesUpload>

  <el-card class="mt10">
    <el-table :data="tableData" border size="small"></el-table>
  </el-card>
  <!-- <el-input v-model="state.person.name"></el-input>
  <el-input v-model="state.person.age"></el-input> -->
</template>
<script setup>
import { watch, reactive } from "vue";
import { ref } from "vue";
// import XLSX from 'xlsx'
import filesUpload from "../../../components/filesUpload.vue";
const importRef = ref("");
const tableData = ref([]);
const importExcel = () => {
  let params = {};
  importRef.value.acceptParams(params);
  console.log(importRef.value.acceptParams(params));
};
const state = reactive({
  firstName: "",
  lastName: "",
  age: 0,
  // person: {
  //   name: "",
  //   age: "444",
  // },
});

const gatewayData = (params) => {
  console.log(params);
};
// watch(
//   [state.person.name, state.person.age],
//   (newValue, oldValue) => {
//     console.log("person变化了", newValue, oldValue);
//   },
//   {
//     immediate: true,
//     // deep: true
//   }
// );
</script>

<style lang="scss" scoped>
.mt-4 {
  float: right;
  text-align: right;
  margin-bottom: 20px;
}
</style>
