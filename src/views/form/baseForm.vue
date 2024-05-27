<template>
  <!-- <el-card class="col-center">
    <el-form :model="form" label-width="120px">
      <el-form-item label="活动名称">
        <el-input v-model="form.name" />
      </el-form-item>
      <el-form-item label="活动区域">
        <el-select v-model="form.region" placeholder="please select your zone">
          <el-option label="区域一" value="shanghai" />
          <el-option label="区域二" value="beijing" />
        </el-select>
      </el-form-item>
      <el-form-item label="活动日期">
        <el-col :span="11">
          <el-date-picker
            v-model="form.date1"
            type="date"
            placeholder="开始日期"
            style="width: 100%"
          />
        </el-col>
        <el-col :span="2" class="开启活动">
          <span class="text-gray-500">-</span>
        </el-col>
        <el-col :span="11">
          <el-time-picker
            v-model="form.date2"
            placeholder="结束日期"
            style="width: 100%"
          />
        </el-col>
      </el-form-item>
      <el-form-item label="活动状态">
        <el-switch v-model="form.delivery" />
      </el-form-item>
      <el-form-item label="活动类型">
        <el-checkbox-group v-model="form.type">
          <el-checkbox label="Online activities" name="type" />
          <el-checkbox label="Promotion activities" name="type" />
          <el-checkbox label="Offline activities" name="type" />
          <el-checkbox label="Simple brand exposure" name="type" />
        </el-checkbox-group>
      </el-form-item>
      <el-form-item label="活动资源">
        <el-radio-group v-model="form.resource">
          <el-radio label="Sponsor" />
          <el-radio label="Venue" />
        </el-radio-group>
      </el-form-item>
      <el-form-item label="活动描述">
        <el-input v-model="form.desc" type="textarea" />
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">创建</el-button>
        <el-button>取消</el-button>
      </el-form-item>
    </el-form>
  </el-card> -->
  <p>带表单验证的</p>
  <el-card class="col-center">
    <el-form
      ref="ruleFormRef"
      :model="ruleForm"
      :rules="rules"
      label-width="120px"
      class="demo-ruleForm"
    >
      <el-form-item label="名字" prop="name">
        <el-input v-model="ruleForm.name" />
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm">验证</el-button>
      </el-form-item>
    </el-form>
  </el-card>
</template>

<script setup>
import { valid } from "mockjs";
import { reactive, ref } from "vue";
const ruleFormRef = ref();
// do not use same name with ref
const form = reactive({
  name: "",
  region: "",
  date1: "",
  date2: "",
  delivery: false,
  type: [],
  resource: "",
  desc: "",
});
const ruleForm = reactive({
  name: "",
});
const nameChange = (rule, value, callback) => {
  if (!value) {
    return callback(new Error("请填写名字"));
  } else {
    return callback();
  }
};
const rules = {
  name: [
    {
      validator: nameChange,
      trigger: "blur",
    },
  ],
};
const submitForm = async () => {
  ruleFormRef.value.validate((valid) => {
    if (valid) {
      alert("ok");
    } else {
      alert("no");
    }
  });
};
const onSubmit = () => {
  console.log("submit!");
};
</script>
