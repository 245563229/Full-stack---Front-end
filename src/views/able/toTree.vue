<template>
  <div
    class="container"
    style="font-size: 20px; color: red; text-align: center"
  >
    树状结构递归生成
  </div>
  <div style="text-align: center">
    <el-button type="primary" @click="createTree">点击生成树状结构</el-button>
  </div>
  <!-- 未树结构表格 -->
  <el-table
    :data="tableData"
    style="width: 100%"
    row-key="id"
    default-expand-all
  >
    <el-table-column prop="id" label="id" width="200" />
    <el-table-column prop="fatherId" label="fatherId" width="100" />
    <el-table-column prop="name" label="备注" />
  </el-table>
</template>

<script setup>
import { create } from "lodash";
import { reactive, ref } from "vue";
const state = reactive({
  newTree: [],
});
//  id  数据id
//  fatherId 子节点所对应的父节点的id，即如果fatherId = 某一项的id。那他就是那一项的子项
//   name  此处用作备注
const tableData = ref([
  {
    id: 1,
    name: "我是父节点1",
    fatherId: 0,
  },
  {
    id: 2,
    name: "我是父节点2",
    fatherId: 0,
  },
  {
    id: 3,
    name: "我是父节点1的子节点1-1",
    fatherId: 1,
  },
  {
    id: 4,
    name: "我是父节点2的子节点2-1",
    fatherId: 2,
  },
  {
    id: 5,
    name: "我是父节点2的子节点2-2",
    fatherId: 2,
  },
  {
    id: 6,
    name: "我是父节点2的子节点2-3",
    fatherId: 2,
  },
  {
    id: 7,
    name: "我是父节点2-3的子节点2-3-1",
    fatherId: 6,
  },
  {
    id: 8,
    name: "我是父节点2-3的子节点2-3-2",
    fatherId: 6,
  },
  {
    id: 9,
    name: "我是父节点2-3-1的子节点2-3-1-1",
    fatherId: 7,
  },
  {
    id: 10,
    name: "我是父节点2-1的子节点2-1-1",
    fatherId: 4,
  },
]);
//生成树状结构
const createTree = () => {
  console.log("我是生成前的结构", tableData.value);
  state.newTree = handleTree(tableData.value, "id", "fatherId");
  console.log("我是生成后的结构", state.newTree);
  setTimeout(() => {
    tableData.value = state.newTree;
  }, 2000);
};
//_________________________________
//  data 数据源
//  id id字段 默认 'id'
//  parentId 父节点字段 默认 'parentId'
//  children 孩子节点字段 默认 'children
//  rootId 根Id 默认 0
const handleTree = (data, id, parentId, children, rootId) => {
  id = id || "id";
  parentId = parentId || "parentId";
  children = children || "children";
  rootId = rootId || 0;
  //对源数据深度克隆
  const cloneData = JSON.parse(JSON.stringify(data));
  //循环所有项
  const treeData = cloneData.filter((father) => {
    let branchArr = cloneData.filter((child) => {
      //返回每一项的子级数组
      return father[id] === child[parentId];
    });
    branchArr.length > 0 ? (father.children = branchArr) : "";
    //返回第一层
    return father[parentId] === rootId;
  });
  return treeData != "" ? treeData : data;
};
</script>

<style scoped lang="scss"></style>
