<template>
  <el-container>
    <el-header style="height:30px" class="app-win-menu-title el-page-header__content">
      <span v-show="extensionShow[settingName]">{{ $t('setting.name') }}</span>
      <span v-show="extensionShow[title[1]] && !extensionIconShow[title[1]]" v-for="title in menuTitles" v-bind:key="typeof title[0] === 'string' ? title[0] : title[0].name">{{typeof title[0] === 'string' ? title[0] : title[0].i18n ? title[0].parentI18n ? $t(`${title[0].name}`) : $t(`${title[1]}.${title[0].name}`) : title[0].name}}</span>
    </el-header>
    <el-main class="app-win-menu-content">
      <setting-menu v-show="extensionShow[settingName]"/>
      <component v-show="extensionShow[menu[1]] && !extensionIconShow[menu[1]]" v-for="menu in menus" v-bind:key="menu[0]" v-bind:is="menu[0]" ></component>
    </el-main>
  </el-container>
</template>
<script lang="ts">
import Vue from 'vue'
import SettingMenu from './SettingMenu.vue'
import { ExtensionManager } from '@/plugins'
import { SettingConfig } from '@/utils'
import { mapGetters } from 'vuex'
export default Vue.extend({
  data() {
    return {
      menuTitles: ExtensionManager.getMenuTitles(),
      settingName: SettingConfig.SettingName,
      menus: ExtensionManager.getMenus()
    }
  },
  components: {
    SettingMenu
  },
  computed: {
    ...mapGetters([
      'extensionShow',
      'extensionIconShow'
    ])
  }
})
</script>
<style lang="scss" scoped>
  .app-win-menu-title {
    font-size: 16px !important;
    line-height: 30px;
    span {
      height: 30px;
      width: 100%;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      display: block;
    }
  }
  .app-win-menu-content {
    &::-webkit-scrollbar {
      display: none;
    }
  }
</style>
