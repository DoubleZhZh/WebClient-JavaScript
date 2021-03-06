<template>
  <div :class="{'mapgis-header': true, 'mapgis-header-mobile': mobile}">
    <router-link to="/">
      <div class="mapgis-webclient-header">
        <img
          :src="logo"
          class="mapgis-webclient-logo"
        >
        <span
          v-if="!mobile"
          class="mapgis-webclient-text"
        >
          Client for JavaScript
        </span>
      </div>
    </router-link>
    <div class="mapgis-webclient-menu">
      <el-popover
        v-for="(h,i) in mobile ? mobileHeaders : headers"
        :key="i"
        placement="top-start"
        trigger="hover"
      >
        <header-menu
          :menus="h.menus"
          :icon="h.icon"
        />
        <el-button
          type="text"
          slot="reference"
          :class="{'active': isActiveMenu(h.title)}"
        >
          <IconFont
            :type="h.icon"
            class="menu-icon"
          />
          {{h.title}}
        </el-button>
      </el-popover>
      <div v-if="mobile">
        <el-popover
          v-for="h in mobileSubheaders"
          :key="h.title"
          placement="top-start"
          trigger="hover"
        >
          <header-sub-menu
            :active="activeTabs[h.title]"
            :menus="h.menus"
          />
          <el-button
            type="text"
            slot="reference"
          >{{h.title}}</el-button>
        </el-popover>
      </div>
    </div>
  </div>
</template>

<script>
import { isMobile } from "@/utils/mobile";
import { Headers, SubHeader, MobileHeaders, MobileSubHeader } from './config';
import HeaderMenu from './Menu';
import HeaderSubMenu from './SubMenu';
import IconFont from "@/components/IconFont/iconfront";

export default {
  components: {
    IconFont,
    HeaderMenu,
    HeaderSubMenu,
  },
  data () {
    return {
      mobile: isMobile(),
      logo: './static/assets/logo/mapgis_blue.png',
      activeMenu: '',
      activeTabs: {},
      headers: Headers,
      subheaders: SubHeader,
      mobileHeaders: MobileHeaders,
      mobileSubheaders: MobileSubHeader,
    };
  },
  created () {
    const headers = isMobile() ? MobileSubHeader : SubHeader;
    headers.forEach((h) => {
      this.activeTabs[h.title] = h.active.toLowerCase();
    });
  },
  mounted () {
    this.activeMenu = this.$route.params.mapmode.toLowerCase();
  },
  watch: {
    '$route' (to, from) {
      // 对路由变化作出响应...
      let mapmode = to.params.mapmode
      if (mapmode !== from.params.mapmode) {
        const headers = this.mobile ? MobileSubHeader : SubHeader;
        this.activeMenu = mapmode.toLowerCase();
        headers.forEach(header => {
          header.menus.forEach(m => {
            let active = m.title.toLowerCase();
            if (active === mapmode) {
              this.activeTabs[header.title] = active
            }
          })
        });
      }
    },
  },
  methods: {
    isActiveTab (title) {
      title = title.toLowerCase()
      Object.keys(this.activeTabs).forEach(key => {
        let active = this.activeTabs[key]
        if (title.indexOf(active) >= 0) {
          return true;
        }
      })
      return false;
    },
    isActiveMenu (title) {
      if (!this.activeMenu || !title) return false
      title = title.toLowerCase();
      if (title.indexOf(this.activeMenu) >= 0) {
        return true
      }
      return false
    }
  }
}
</script>

<style lang="scss">
.mapgis-header-mobile {
  height: 48px !important;
  .mapgis-webclient-logo {
    margin-left: 22px !important;
    height: 24px !important;
  }
  .mapgis-webclient-header {
    width: fit-content;
    height: 48px !important;
  }
  .mapgis-webclient-menu {
    margin-right: 22px !important;
  }
  .mapgis-webclient-menu {
    height: 48px !important;
    span {
      font-size: 13px !important;
    }
  }
}
.mapgis-header {
  font-family: Microsoft YaHei;
  width: 100%;
  padding: 0px !important;
  height: 72px;
  background: rgba(37, 45, 69, 1);

  .mapgis-webclient-header {
    width: fit-content;
    height: 72px;
    align-items: center;
    float: left;
    display: flex;
    background: transparent;

    .mapgis-webclient-logo {
      margin-left: 81px;
      height: 38px;
    }
    .mapgis-webclient-text {
      width: fit-content;
      height: 24px;
      margin-left: 13px;
      color: rgba(255, 255, 255, 1);
      line-height: 24px;
      font-size: 22px;
      font-weight: bold;
      font-style: italic;
      font-stretch: normal;
      letter-spacing: 1.5px;
    }
    .menu-icon {
      margin-right: 8px !important;
    }
  }

  .mapgis-webclient-menu {
    width: fit-content;
    margin-right: 92px;
    height: 72px;
    align-items: center;
    float: right;
    display: flex;

    span {
      width: fit-content;
      // height: 16px;
      margin: 0px 6px;
      padding: 0px 2px;
      // margin-left: 12.5px;
      font-size: 16px;
      font-family: Microsoft YaHei;
      font-weight: 500;
      text-align: right;
      color: rgba(255, 255, 255, 1);
      line-height: 20px;
    }

    span:hover {
      color: #33dbe8;
    }

    .active {
      border-radius: 0px;
      border-bottom: 3px solid #33dbe8;
      span {
        color: #33dbe8 !important;
        font-size: bold;
      }
    }
  }
}
</style>