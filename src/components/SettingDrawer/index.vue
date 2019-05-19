<template>
  <div>
    <a-drawer
      placement="right"
      :closable="false"
      @close="onClose"
      :visible="visible"
      width="300px"
    >
      <template v-slot:handle>
        <div class="setting-drawer-handle" @click="visible = !visible">
          <a-icon :type="visible ? 'close' : 'setting'"></a-icon>
        </div>
      </template>
      <div>
        <div>
          <h2>整体风格定制</h2>
          <a-radio-group
            :value="$route.query.navTheme || 'dark'"
            @change="e => handleSettingChange('navTheme', e.target.value)"
          >
            <a-radio value="dark">黑色</a-radio>
            <a-radio value="light">白色</a-radio>
          </a-radio-group>
          <h2>导航模式</h2>
          <a-radio-group
            :value="$route.query.navLayout || 'left'"
            @change="e => handleSettingChange('navLayout', e.target.value)"
          >
            <a-radio value="left">左侧</a-radio>
            <a-radio value="top">顶部</a-radio>
          </a-radio-group>
          <h2>主题颜色</h2>
          <div>
            <template v-for="tag in colorThemeTags">
              <a-tooltip :key="tag" :title="tag">
                <a-tag
                  style="margin: 10px"
                  @click="handleSettingChange('themeColor', tag)"
                  :color="tag"
                  >{{ themeColor === tag ? "√" : "&nbsp;&nbsp;" }}</a-tag
                >
              </a-tooltip>
            </template>
          </div>
        </div>
      </div>
    </a-drawer>
  </div>
</template>
<script>
export default {
  data() {
    return {
      visible: false,
      colorThemeTags: [
        "pink",
        "red",
        "orange",
        "cyan",
        "blue",
        "purple",
        "#f50",
        "#2db7f5",
        "#87d068",
        "#108ee9"
      ]
    };
  },
  computed: {
    themeColor() {
      if (this.$route.query.themeColor) {
        return this.$route.query.themeColor;
      }
      return this.colorThemeTags[0];
    }
  },
  methods: {
    onClose() {
      this.visible = false;
    },
    handleSettingChange(type, value) {
      this.$router.push({ query: { ...this.$route.query, [type]: value } });
    }
  }
};
</script>
<style lang="less" src="./index.less"></style>
