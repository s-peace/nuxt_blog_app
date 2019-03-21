<template>
  <section class="container posts-page">
    <el-card>
      <div slot="header" class="Clearfix"></div>
      <span>add new post</span>
    </el-card>
    <el-table
      :data="showPosts"
      style="width:100%"
      class='table'
    >
      <el-table-column
        prop="title"
        label="title"
      >
      </el-table-column>
      <el-table-column
        prop="user.id"
        label="editor"
        width: 180px
      >
      </el-table-column>
      <el-table-column
        prop="created_at"
        label="added date"
        width: 240px
      >
      </el-table-column>
    </el-table>
  </section>
</template>

<script>
export default {
  computed: {
    showPosts() {
      return [
        {
          id: '001',
          title: 'test1',
          body: 'test11111111111111111111111111111111111111111111',
          created_at: '2018/10/10 12:00:00',
          user: {
            id: 'aaa'
          }
        },
        {
          id: '002',
          title: 'test2',
          body: 'test222222222222222222222222222222222222222222222',
          created_at: '2019/1/10 22:22:22',
          user: {
            id: 'aaa'
          }
        }
      ]
    }
  }
}
</script>

<style>
.posts-page .el-table__row {
  cursor: pointer;
}
</style>
