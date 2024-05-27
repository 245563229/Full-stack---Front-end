<template>
  <el-card class="box-card col-center" shadow="never">
    <a
      href="https://openplatform-portal.dg-work.cn/portal/#/helpdoc?apiType=jsapi&docKey=2675393"
      target="three"
      >9999</a
    >
    <span class="box-card-title">富文本编辑器 🍰🍰🍰🍩🍩🍩</span>
    <button @click="getEditorContent">获取富文本内容</button>
    <div class="wangeditor-box">
      <Toolbar
        style="border-bottom: 1px solid #ccc"
        :editor="editorRef"
        :defaultConfig="toolbarConfig"
        :mode="mode"
      />
      <Editor
        class="editor-txt"
        v-model="valueHtml"
        :defaultConfig="editorConfig"
        :mode="mode"
        @onCreated="handleCreated"
      />
    </div>
  </el-card>
</template>

<script setup>
import "@wangeditor/editor/dist/css/style.css"; // 引入 css
import { onBeforeUnmount, ref, shallowRef, onMounted } from "vue";
import { Editor, Toolbar } from "@wangeditor/editor-for-vue";
const editorRef = shallowRef();

// 内容 HTML
const valueHtml = ref("<p>hello</p>");
const getEditorContent = () => {
  console.log("valueHtml", valueHtml.value);
};
const ccc =
  '<p>富文本编辑器</p><p><img src="https://seopic.699pic.com/photo/50051/5435.jpg_wh1200.jpg" alt="" data-href="" style=""/></p><p>富文本编辑器</p>';
// 模拟 ajax 异步获取内容
onMounted(() => {
  setTimeout(() => {
    // valueHtml.value = ccc;
  }, 1500);
});
{
  /* <img src="../../assets/bg.png" />; */
}
const toolbarConfig = {};
const editorConfig = { placeholder: "请输入内容..." };

// 组件销毁时，也及时销毁编辑器
onBeforeUnmount(() => {
  const editor = editorRef.value;
  if (editor == null) return;
  editor.destroy();
});

const handleCreated = (editor) => {
  editorRef.value = editor; // 记录 editor 实例，重要！
};
</script>

<style lang="scss" scoped>
.box-card {
  width: 100%;
  .wangeditor-box {
    border: 1px solid #f0f2f5;
    margin-top: 20px;
  }
  .editor-txt {
    height: 75vh !important;
    overflow-y: hidden;
    text-align: left;
  }
}
img {
  width: 50px;
  height: 50px;
}
</style>
