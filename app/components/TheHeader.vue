<template>
  <el-menu mode="horizontal" :router="true">
    <el-menu-item index="1" style="pointer-events:none;">
      Nuxt Diary App
    </el-menu-item>
    <el-menu-item index="2" :route="{path: '/posts'}">
      posts list
    </el-menu-item>

    <no-ssr>
      <el-menu-item index="4" style="float: right;" :route="{path:'/'}">
        <span>login</span>
      </el-menu-item>
      <el-menu-item index="5" style="float: right;" :route="{path: '/posts/new'}">
        post new
      </el-menu-item>
    </no-ssr>
  </el-menu>
</template>
