<template>
  <a-layout id="base-layout">
    <a-layout-header class="header">
      <div class="logo">
        <span class="logo-text">MechMarket</span>
      </div>
    </a-layout-header>
    <a-layout>
      <a-layout-sider collapsible>
        <a-menu
          mode="inline"
          :defaultSelectedKeys="['1']"
          :defaultOpenKeys="['sub1']"
          :style="{ height: '100%', borderRight: 0 }"
          theme="light"
        >
          <a-sub-menu key="sub1">
            <span slot="title">
              <a-icon type="user" />
              <span>Sort by Region</span>
            </span>
            <a-menu-item key="1" v-on:click="setPrefCookie('all')">All</a-menu-item>
            <a-menu-item key="2" v-on:click="setPrefCookie('usa')">United States</a-menu-item>
            <a-menu-item key="3" v-on:click="setPrefCookie('can')">Canada</a-menu-item>
            <a-menu-item key="4" v-on:click="setPrefCookie('aus')">Australia</a-menu-item>
            <a-menu-item key="5" v-on:click="setPrefCookie('eur')">Europe</a-menu-item>
          </a-sub-menu>
          <a-sub-menu key="sub2">
            <span slot="title">
              <a-icon type="laptop" />
              <span>Sort by flair</span>
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


<style lang="scss">
.logo-text {
  color: white;
}

.header {
  border-bottom: 5px;
  border-color: white;
}

a-layout-slider {
  width: 200px;
}
</style>


<script>
import Posts from "~/components/posts.vue";
export default {
  components: {
    Posts,
  },

  data() {
    return {
      collapsed: true,
    };
  },
  methods: {
    // Called when clicking on a region in the sidebar to set it as a preference.
    setPrefCookie: function (token) {
      localStorage.setItem("country", token);
    },
  },
  mounted() {
    //Set the default option for country to all if localStorage key doesn't exist.
    if (localStorage.getItem("country") === null) {
      localStorage.setItem("country", "all");
    }
  },
};
</script>
