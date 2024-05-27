<template>
  <div :class="state.newClass">
    <span :style="state.IconClass" class="IconClass"> </span>
    <slot></slot>
  </div>
</template>
<script setup>
import { ref, reactive, onMounted } from "vue";
const props = defineProps({
  color: {
    type: String,
    request: true,
  },
  //尺寸设定
  size: {
    type: String,
  },
  //右边距
  marginRight: {
    type: String,
  },
  //自定义class
  class: {
    type: Object,
  },
});
const state = reactive({
  //默认打点尺寸
  IconClass: {
    width: props.size || "6px",
    height: props.size || "6px",
    borderRadius: props.size || "3px",
    marginRight: props.marginRight || "5px",
    backgroundColor: props.color,
  },
  newClass: props.class,
});
</script>
<style scoped lang="scss">
.IconClass {
  display: inline-block;
}
</style>
