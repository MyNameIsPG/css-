<template>
  <div class="button-nav-btn bounceInRight animated">
    <ul class="button-nav-btn-list">
      <template v-for="(item, index) in menu['menus' + currentKey]">
        <li
          class="item"
          :key="index"
          :class="item.path === $route.path ? 'active' : ''"
          @click="handelClick(index, item)"
        >
          <div class="icon">
            <i class="icon iconfont" :class="item.icon"></i>
          </div>
          <p class="text">{{ item.name }}</p>
        </li>
      </template>
    </ul>
  </div>
</template>

<script>
export default {
  name: "SideMenus",
  data() {
    return {
      currentKey: 0,
      menu: {
        menus0: [
          {
            name: "查询与统计",
            icon: "icon-tongji",
            path: "/home/design/queryAndStatistics",
          },
          {
            name: "现场踏勘",
            icon: "icon-15takan",
            path: "/home/design/siteSurvey",
          },
          {
            name: "施工进度模拟",
            icon: "icon-construction",
            path: "/home/design/simulation",
          },
          { name: "拆迁进度监控", icon: "icon-jindu", path: "/home/design/demolition" },
        ],
        menus1: [
          {
            name: "项目概况",
            icon: "icon-icon-project1",
            path: "/home/constructions/projectOverview",
          },
          {
            name: "项目风采",
            icon: "icon-qiyefengcai",
            path: "/home/constructions/styleOfTheProject",
          },
          {
            name: "关键工程",
            icon: "icon-gongcheng",
            path: "/home/constructions/keyProjects",
          },
          {
            name: "投资控制",
            icon: "icon-touzi",
            path: "/home/constructions/investmentControl",
          },
          {
            name: "形象控制",
            icon: "icon-jindu2",
            path: "/home/constructions/imageControl",
          },
          {
            name: "质量管理",
            icon: "icon-zhiliang1",
            path: "/home/constructions/qualityAssurance",
          },
          {
            name: "安全管理",
            icon: "icon-zhiliang",
            path: "/home/constructions/securityManagement",
          },
          {
            name: "视频管理",
            icon: "icon-shipin",
            path: "/home/constructions/videoManagement",
          },
        ],
        menus2: [
          { name: "首页", icon: "icon-shouye", path: "/home/liangchang/liangchangIndex" },
          {
            name: "梁片管理",
            icon: "icon-zhichengliang",
            path: "/home/liangchang/PieceManagement",
          },
          {
            name: "安全监控",
            icon: "icon-jiankong",
            path: "/home/liangchang/safetyMonitoring",
          },
          { name: "预警信息", icon: "icon-yujing", path: "/home/liangchang/Warning" },
          {
            name: "信息溯源",
            icon: "icon-suyuan",
            path: "/home/liangchang/informationTrace",
          },
        ],
        menus3: [],
      },
    };
  },
  created() {
    this.getRouteIndex(this.$route.path);
  },
  methods: {
    handelClick(index, item) {
      if (item.path) {
        this.$router.push({ path: item.path });
      }
      this.$emit("change", item);
    },
    getRouteIndex(path) {
      if (path.indexOf("design") != -1) {
        this.currentKey = 0;
      } else if (path.indexOf("constructions") != -1) {
        this.currentKey = 1;
      } else if (path.indexOf("liangchang") != -1) {
        this.currentKey = 2;
      } else if (path.indexOf("curing") != -1) {
        this.currentKey = 3;
      }
    },
  },
  watch: {
    $route(route) {
      this.getRouteIndex(route.path);
    },
  },
};
</script>

<style lang="sass" scoped>
.button-nav-btn
  position: absolute
  right: 30px
  bottom: 20px
  z-index: 9999
  .button-nav-btn-list
    display: flex
    .item
      padding: 0 15px
      cursor: pointer
      transition: all .5s
      .icon
        width: 60px
        height: 55px
        display: flex
        justify-content: center
        align-items: center
        margin: 0 auto
        transition-duration: .5s
        background: url(../assets/img/siderightmenu/btn-bg.png) no-repeat
        i
          transition-duration: .5s
          font-size: 28px
          color: #26ceff
      .text
        color: #fefefe
        font-size: 16px
        text-align: center
        margin-top: 10px
        transition-duration: .5s
      &:hover,
      &.active
        .icon
          background: url(../assets/img/siderightmenu/btn-bg-h.png) no-repeat
          i
            color: #fff200
        .text
          color: #ffde3d
      &:hover
        transform: scale(1.1)
</style>
