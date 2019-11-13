<template>
  <div :class="{'has-logo':showLogo}">
    <logo v-if="showLogo" :collapse="isCollapse" />
    <!-- 登录显示头像昵称 -->
    <div class="head-log">
      <div class="head-img">👮</div>
      <div class="nick-name">警察</div>
    </div>

    <el-scrollbar wrap-class="scrollbar-wrapper">
      <el-menu
        :default-active="activeMenu"
        :collapse="isCollapse"
        :background-color="variables.menuBg"
        :text-color="variables.menuText"
        :unique-opened="false"
        :active-text-color="variables.menuActiveText"
        :collapse-transition="false"
        mode="vertical"
      >
        <sidebar-item
          v-for="route in routes"
          :key="route.path"
          :item="route"
          :base-path="route.path"
        />
      </el-menu>
    </el-scrollbar>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import Logo from "./Logo";
import SidebarItem from "./SidebarItem";
import variables from "@/styles/variables.scss";

export default {
  components: { SidebarItem, Logo },
  computed: {
    ...mapGetters(["sidebar"]),
    routes() {
      return this.$router.options.routes;
    },
    activeMenu() {
      const route = this.$route;
      const { meta, path } = route;
      // if set path, the sidebar will highlight the path you set
      if (meta.activeMenu) {
        return meta.activeMenu;
      }
      return path;
    },
    showLogo() {
      return this.$store.state.settings.sidebarLogo;
    },
    variables() {
      return variables;
    },
    isCollapse() {
      return !this.sidebar.opened;
    }
  }
};
</script>
<style scoped lang="scss">
.head-log {
  box-sizing: border-box;
  height: 90px;
  background: menuHover;
  color: whitesmoke;
  font-size: 28px;
  line-height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  .head-img {
    width: 50px;
    height: 50px;
    text-align: center;
    background: wheat;
    border-radius: 50%;
  }
  .nick-name {
    font-size: 14px;
    width: 50px;
    height: 20px;
    background: menuHover;
    color: whitesmoke;
    text-align: center;
    line-height: 20px;
    padding: 10px 0;
  }
}
</style>
