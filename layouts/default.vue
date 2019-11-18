<template>
  <a-layout id="base-layout">
    <a-layout-header class="header">
      <div class="logo">
        <span class="logo-text">MechMarket</span>
      </div>
    </a-layout-header>
    <a-layout>
      <a-layout-sider width="200" style="background: #fff">
        <a-menu
          mode="inline"
          :defaultSelectedKeys="['1']"
          :defaultOpenKeys="['sub1']"
          :style="{ height: '100%', borderRight: 0 }"
          theme="light"
        >
          <a-sub-menu key="sub1">
            <span slot="title">
              <a-icon type="user" />Sort by Region
            </span>
            <a-menu-item key="1">All</a-menu-item>
            <a-menu-item key="2">United States</a-menu-item>
            <a-menu-item key="3">Canada</a-menu-item>
            <a-menu-item key="4">Australia</a-menu-item>
            <a-menu-item key="5">Europe</a-menu-item>
          </a-sub-menu>
          <a-sub-menu key="sub2">
            <span slot="title">
              <a-icon type="laptop" />Sort by Flair
            </span>
            <a-menu-item key="6">Interest Check</a-menu-item>
            <a-menu-item key="7">Group Buy</a-menu-item>
            <a-menu-item key="8">Selling</a-menu-item>
            <a-menu-item key="9">Buying</a-menu-item>
            <a-menu-item key="10">Trading</a-menu-item>
          </a-sub-menu>
        </a-menu>
      </a-layout-sider>
      <a-layout style="padding: 0 24px 24px">
        <a-layout-content
          :style="{ background: '#fff', padding: '24px', margin: 0, minHeight: '280px' }"
        >
          <posts />
        </a-layout-content>
      </a-layout>
    </a-layout>
  </a-layout>
</template>
<script>
export default {
  data() {
    return {
      collapsed: false
    };
  }
};
</script>

<style lang="scss">
.logo-text {
  color: white;
}

.header {
  border-bottom: 5px;
  border-color: white;
}
</style>

<script>
import Posts from "~/components/posts.vue";

export default {
  components: {
    Posts
  }
};
</script>
