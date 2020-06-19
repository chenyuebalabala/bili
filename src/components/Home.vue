<template>
<el-container class="home-comtainer">
  <el-header>
      <div>
          <img src="../assets/logo.png" alt="">
          <span>电商后台管理系统</span>
      </div>
      <el-button type="info" @click="logout">退出</el-button>
  </el-header>
  <el-container>
    <el-aside width="200px">
        <!-- 侧边栏菜单区 -->
        <el-menu
      background-color="#333744"
      text-color="#fff"
      active-text-color="red">
      <!-- 一级菜单 -->
      <el-submenu :index="item.id + ''" v-for="item in menulist" :key="item.id">
          <!-- 一级菜单模版 -->
        <template slot="title">
            <!-- 图标 -->
          <i class="el-icon-location"></i>
          <!-- 文本 -->
          <span>{{item.authName}}</span>
        </template>

            <!-- 二级菜单 -->
            <el-submenu :index="subItem.id + ''" v-for="subItem in item.children" :key="subItem.id">
                <template slot="title">
                    <!-- 图标 -->
                <i class="el-icon-location"></i>
                <!-- 文本 -->
                <span>{{subItem.authName}}</span>
                </template>
            </el-submenu>
      </el-submenu>
    </el-menu>
    </el-aside>
    <el-main>Main</el-main>
  </el-container>
</el-container>
</template>

<script>
export default {
  data () {
    // 这里存放数据
    return {
      // 左侧菜单数据
      menulist: []
    }
  },
  created () {
    this.getMenuList()
  },
  methods: {
    logout () {
      window.sessionStorage.clear()
      this.$router.push('/login')
    },
    // 获取所有的菜单
    async getMenuList () {
      const { data: res } = await this.$http.get('menus')
      if (res.meta.status !== 200) return this.$message.error(res.meta.msg)
      this.menulist = res.data
      console.log(res)
    }
  }
}
</script>
<style lang='less' scoped>
.home-comtainer{
    height: 100%;
}
.el-header{
    background-color: #373d41;
    // 在弹性盒对象的 <div> 元素中的各项周围留有空白：
    display: flex;
    justify-content: space-between;
    padding-left: 0;
    align-items: center;
    color: #fff;
    font-size: 20px;
    > div {
        display: flex;
        align-items: center;
      span {
          margin-left: 15px;
      }
    }
}

.el-aside{
    background-color: #333744;
}

.el-main{
    background-color: #eaedf1;
}
</style>
