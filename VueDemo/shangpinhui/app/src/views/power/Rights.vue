<template>
  <div>
    <!-- 头部面包屑导航 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>权限管理</el-breadcrumb-item>
      <el-breadcrumb-item>权限列表</el-breadcrumb-item>
    </el-breadcrumb>

    <!-- 中间卡片区域 -->
    <el-card class="box-card">
      <el-table :data="rights" style="width: 100%" border stripe>
        <el-table-column type="index" label="#"></el-table-column>
        <el-table-column prop="authName" label="权限名称"></el-table-column>
        <el-table-column prop="path" label="路径"></el-table-column>
        <el-table-column prop="level" label="权限等级">
          <template slot-scope="scoped">
            <el-tag v-if="scoped.row.level=='0'" type="success">一级</el-tag>
            <el-tag v-else-if="scoped.row.level=='1'" type="success">二级</el-tag>
            <el-tag v-else type="waring">三级</el-tag>
          </template>
        </el-table-column>
      </el-table>
    </el-card>
  </div>
</template>

<script>
export default {
  name: "Rights",
  data() {
    return {
      rights: [],
    };
  },
  methods: {
    async getRightsList() {
      const { data: res } = await this.$http.get("rights/list");
      if (res.meta.status != 200) {
        return this.$message.error("获取right列表失败");
      }
      this.rights = res.data;
    },
  },
  created() {
    this.getRightsList();
  },
};
</script>

<style>
</style>