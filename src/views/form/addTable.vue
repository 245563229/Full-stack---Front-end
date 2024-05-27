<template>
  <el-card class="contentAll">
    <el-button type="primary" @click="addLineSell">添加一行</el-button>
    <el-button type="primary" @click="submitForm"
      >提交表单验证并获取tabel数据</el-button
    >

    <el-form
      label-width="135px"
      class="demo-ruleForm"
      :size="formSize"
      status-icon
    >
      <div>
        <el-form
          class="base-form"
          ref="baseFormSell"
          :model="state.baseFormSell"
          auto-complete="on"
          :rules="rulesChildren"
        >
          <el-table
            style="width: 100%; margin-bottom: 20px"
            :data="state.baseFormSell.demoList"
            row-key="idKey"
            border
            default-expand-all
          >
            <el-table-column :label="'名称'" min-width="110">
              <template #default="scope">
                <el-form-item
                  v-if="scope.row.disEdit"
                  :prop="'demoList.' + scope.$index + '.name'"
                  :rules="rulesChildren.name"
                >
                  <el-input
                    v-model="scope.row.name"
                    placeholder="请输入"
                    clearable
                  ></el-input>
                </el-form-item>
                <span v-else>{{ scope.row.name }}</span>
              </template>
            </el-table-column>
            <el-table-column label="资产类型" min-width="110">
              <template #default="scope">
                <el-form-item
                  :prop="'demoList.' + scope.$index + '.mark'"
                  :rules="rulesChildren.mark"
                  v-if="scope.row.disEdit"
                >
                  <el-select
                    filterable
                    v-model="scope.row.mark"
                    placeholder="请选择"
                  >
                    <el-option
                      v-for="item in state.dictionary.buildPropertyType"
                      :key="item.value"
                      :label="item.label"
                      :value="item.value"
                    />
                  </el-select>
                </el-form-item>
                <span v-else>{{
                  buildPropertyTypeStatus(scope.row.mark)
                }}</span>
              </template>
            </el-table-column>
            <el-table-column label="设计建筑面积m²" min-width="120">
              <template #default="scope">
                <el-form-item
                  v-if="scope.row.disEdit"
                  :prop="'demoList.' + scope.$index + '.designArea'"
                  class="all"
                >
                  <el-input-number
                    v-model="scope.row.designArea"
                    placeholder="请输入"
                    clearable
                    :controls="false"
                  ></el-input-number>
                </el-form-item>
                <span v-else>{{ scope.row.designArea }}</span>
              </template>
            </el-table-column>
            <el-table-column label="设计套内面积m²" min-width="120">
              <template #default="scope">
                <el-form-item
                  :prop="'demoList.' + scope.$index + '.designInteriorArea'"
                  class="all"
                  v-if="scope.row.disEdit"
                >
                  <el-input-number
                    v-model="scope.row.designInteriorArea"
                    placeholder="请输入"
                    clearable
                    :controls="false"
                  ></el-input-number>
                </el-form-item>
                <span v-else>{{ scope.row.designInteriorArea }}</span>
              </template>
            </el-table-column>
            <el-table-column label="业态" min-width="110">
              <template #default="scope">
                <el-form-item
                  :prop="'demoList.' + scope.$index + '.format'"
                  v-if="scope.row.disEdit"
                >
                  <el-select
                    filterable
                    v-model="scope.row.format"
                    placeholder="请选择"
                  >
                    <el-option
                      v-for="item in state.dictionary.buildFormat"
                      :key="item.value"
                      :label="item.label"
                      :value="item.value"
                    />
                  </el-select>
                </el-form-item>
                <span v-else>{{ buildFormatStatus(scope.row.format) }}</span>
              </template>
            </el-table-column>
            <el-table-column label="操作" min-width="180">
              <template #default="scope">
                <el-button
                  type="primary"
                  text
                  @click="removeFundBtnSell(scope.$index)"
                  v-if="!scope.row.disEdit"
                  >删除</el-button
                >
                <el-button
                  type="primary"
                  text
                  @click="handleEdit(scope.row)"
                  v-if="!scope.row.disEdit"
                  >修改</el-button
                >
                <el-button
                  type="primary"
                  text
                  @click="handleSave(scope.row)"
                  v-if="scope.row.disEdit"
                  >保存</el-button
                >
              </template>
            </el-table-column>
          </el-table>
        </el-form>
      </div>
    </el-form>
  </el-card>
</template>
<script setup>
import { reactive, ref } from "vue";
import { ElMessage } from "element-plus";
const formSize = ref("default");
const baseFormSell = ref(null);
const state = reactive({
  //字典集合
  dictionary: {
    //资产类型字典
    buildPropertyType: [
      { value: "1", label: "资产类型1" },
      { value: "2", label: "资产类型2" },
    ],
    //业态字典
    buildFormat: [
      {
        value: 1,
        label: "业态类型1",
      },
      {
        value: 2,
        label: "业态类型2",
      },
    ],
  },
  //出售模块
  baseFormSell: {
    demoList: [],
  },
});
const rulesChildren = reactive({
  name: [{ required: true, message: "请输入建筑名", trigger: "blur" }],
  mark: [{ required: true, message: "请选择资产类型", trigger: "change" }],
});
//修改按钮
const handleEdit = (row) => {
  let ifEdit = false;
  state.baseFormSell.demoList.forEach((item) => {
    if (item.disEdit == true) {
      ifEdit = true;
      ElMessage({
        message: "请先保存上一项",
        type: "error",
      });
    }
  });
  if (ifEdit) return;
  baseFormSell.value.validate((valid) => {
    if (valid) {
      row.disEdit = true;
    } else {
      ElMessage({
        message: "请检查必填项",
        type: "error",
      });
    }
  });
};
//保存rentList
const handleSave = (row) => {
  baseFormSell.value.validate((valid) => {
    if (valid) {
      row.disEdit = false;
    } else {
      ElMessage({
        message: "请检查必填项",
        type: "error",
      });
    }
  });
};
// 删除指定行
const removeFundBtnSell = (index) => {
  state.baseFormSell.demoList.splice(index, 1);
};
// 增加一个空行, 用于录入或显示第一行
const addLineSell = () => {
  let ifAdd = false;
  state.baseFormSell.demoList.forEach((item) => {
    if (item.disEdit == true) {
      ifAdd = true;
      ElMessage({
        message: "请先保存上一项",
        type: "error",
      });
    }
  });
  if (ifAdd) return;
  const newLine = {
    idKey: state.baseFormSell.demoList.length + 1,
    //门牌名称
    name: "",
    //资产类型
    mark: "",
    //设计建筑面积
    designArea: "",
    //设计套内面积
    designInteriorArea: "",
    //业态
    format: "",
    disEdit: true,
  };
  state.baseFormSell.demoList.push(newLine);
};
//提交获取tabel数据
const submitForm = () => {
  if (state.baseFormSell.demoList.length < 1) {
    ElMessage({
      message: "请新建行",
      type: "error",
    });
    return;
  }
  const ifPostSell = state.baseFormSell.demoList.findIndex(
    (item) => item.disEdit == true
  );
  console.log("ifPostSell", ifPostSell);
  if (ifPostSell != -1) {
    ElMessage({
      message: "请保存所有项",
      type: "error",
    });
    return;
  }
  baseFormSell.value.validate((valid) => {
    if (valid) {
      console.log("表格数据", state.baseFormSell.demoList);
    } else {
      ElMessage({
        message: "请检查必填项",
        type: "error",
      });
    }
  });
};
//字典翻译
const selectDictLabel = (datas, value) => {
  var actions = [];
  Object.keys(datas).map((key) => {
    if (datas[key].value == "" + value) {
      actions.push(datas[key].label);
      return false;
    }
  });
  return actions.join("");
};

//字典翻译
//资产类型
const buildPropertyTypeStatus = (row, column) => {
  return selectDictLabel(state.dictionary.buildPropertyType, row);
};
//业态
const buildFormatStatus = (row, column) => {
  return selectDictLabel(state.dictionary.buildFormat, row);
};
</script>
<style lang="scss" scoped>
.tableClass {
  &:deep(.el-table__expand-icon) {
    display: inline-block;
  }
}
.imgClass {
  display: inline-block;
  width: 90px;
  height: 42px;
}
:deep(.el-input__inner) {
  text-align: left;
}
</style>
