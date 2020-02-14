<template>
  <div class="home-container">
    <el-container class="home-container">
      <!-- 头部区域 -->
      <el-header>
        <div>
          <img src="../assets/img/h-logo.png" alt="" width="50px" height="50px" border-radius="50%">
          <span>歐美影音周邊后台管理系统</span>
        </div>
        <el-button style="background-color: #dbe9f0" @click="logout">退出</el-button>
      </el-header>
      <!-- 页面主体区域 -->
      <el-container>
        <!-- 侧边栏区域 -->
        <el-aside :width="isCollapse ? '64px' : '200px'">
          <div class="toggle-button" @click="toggleCollapse">|||</div>
          <!-- 側邊欄菜單區 -->
          <el-menu background-color="#dbe9f0" text-color="#2c3e50" active-text-color="#37a3b7" :unique-opened="true" :collapse="isCollapse" :collapse-transition="false" :router="true" :default-active="activePath" >
          <!-- 一级菜单 -->
          <el-submenu :index="item.id + '' " v-for="item in menulist" :key="item.id">
            <!-- 一级菜单模板区 -->
            <template slot="title">
              <!-- 图标 -->
              <i :class="iconsObj[item.id]"></i>
              <!-- 文本 -->
              <span>{{ item.authName }}</span>
            </template>
            <!-- 二级菜单 -->
            <el-menu-item :index="'/' + subItem.path" v-for="subItem in item.children" :key="subItem.id" @click="saveNavState('/' + subItem.path)">
              <template slot="title">
                <!-- 二级图标 -->
                <i class="el-icon-menu"></i>
                <!-- 二级文本 -->
                <span>{{ subItem.authName }}</span>
              </template>
            </el-menu-item>
          </el-submenu>
          </el-menu>
        </el-aside>
        <!-- 主要内容 -->
        <el-main>
          <!-- 路由占位符 -->
          <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
export default {
  data () {
    return {
      // 左侧菜单数据
      menulist: [],
      iconsObj: {
        125: 'iconfont icon-user',
        103: 'iconfont icon-tijikongjian',
        101: 'iconfont icon-shangpin',
        102: 'iconfont icon-danju',
        145: 'iconfont icon-baobiao'
      },
      // 是否折叠
      isCollapse: false,
      // 被激活的链接地址
      activePath: ''
    }
  },
  created () {
    this.getMenuList()
    this.activePath = window.sessionStorage.getItem('activePath')
  },
  methods: {
    logout () {
      window.sessionStorage.clear()
      this.$router.push('/login')
    },
    // 获取所有菜单
    async getMenuList () {
      const { data: res } = await this.$http.get('menus')
      if (res.meta.status !== 200) return this.$message.error(res.meta.msg)
      this.menulist = res.data
      // console.log(res)
    },
    // 折叠
    toggleCollapse () {
      this.isCollapse = !this.isCollapse
    },
    // 保存链接的激活状态
    saveNavState (activePath) {
      window.sessionStorage.setItem('activePath', activePath)
      this.activePath = activePath
    }
  }
}
</script>

<style lang="less" scoped>
  .home-container{
    height: 100%;
  }
  .el-header{
    background-color: #bbe6d6;
    display: flex;
    justify-content: space-between;
    padding-left: 0;
    align-items: center;
    font-size:20px;
    >div {
      display: flex;
      align-items: center;
      span{
        margin-left:15px;
      }
    }
  }
  .el-aside{
    background-color: #dbe9f0;
  }
  .el-main{
    background-color: #c8ebdf;
  }
  .iconfont{
    margin-right: 8px;
  }

  .toggle-button{
    background-color: #b9dace;
    font-size: 10px;
    line-height: 24px;
    text-align: center;
    color: #000;
    letter-spacing: 0.2em;
    cursor: pointer;
  }
</style>
