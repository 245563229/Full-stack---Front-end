<template>
  <template v-for="subItem in menuList" :key="subItem.path">
    <el-sub-menu
      v-if="subItem.children && subItem.children.length > 0"
      :index="subItem.path"
    >
      <template #title>
        <el-icon>
          <component :is="subItem.meta.icon"></component>
        </el-icon>
        <span>{{ subItem.meta.title }}</span>
      </template>
      <Menu-items :menuList="subItem.children"></Menu-items>
      <!--<template v-for="child in subItem.children" :key="child.path">
        <template v-if="child.children && child.children.length > 0">
           <Menu-items :menuList="child.children"></Menu-items>
        </template>
        <el-menu-item v-else :index="child.path">
          <el-icon>
            <component :is="child.meta.icon"></component>
          </el-icon>
          <template #title>
            <span>{{ child.meta.title }}</span>
          </template>
        </el-menu-item>
      </template> -->
    </el-sub-menu>
    <el-menu-item v-else :index="subItem.path">
      <el-icon>
        <component :is="subItem.meta.icon"></component>
      </el-icon>
      <template #title>
        <span>{{ subItem.meta.title }}</span>
      </template>
    </el-menu-item>
  </template>
</template>

<script setup>
defineProps(['menuList'])
</script>

<style scoped>
.icons {
  width: 24px;
  height: 18px;
}
</style>
