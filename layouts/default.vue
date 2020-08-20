<template>
  <a-layout id="base-layout">
    <a-layout-header class="header">
      <div class="header-logo">
        <img src="~/assets/logo.svg" alt="Logo" class="logo" />
        <span class="logo-text">MechMarket</span>
      </div>
    </a-layout-header>
    <a-layout>
      <a-layout-sider collapsible>
        <a-menu
          mode="inline"
          :style="{ height: '100%', borderRight: 0 }"
          theme="light"
          :selectedKeys="countryOption"
        >
          <span slot="title">
            <a-icon type="user" />
            <span>Sort by Region</span>
          </span>
          <a-menu-item key="all" v-on:click="setPrefCookie('all')">All</a-menu-item>
          <a-menu-item key="usa" v-on:click="setPrefCookie('usa')">United States</a-menu-item>
          <a-menu-item key="can" v-on:click="setPrefCookie('can')">Canada</a-menu-item>
          <a-menu-item key="aus" v-on:click="setPrefCookie('aus')">Australia</a-menu-item>
          <a-menu-item key="eur" v-on:click="setPrefCookie('eur')">Europe</a-menu-item>
        </a-menu>
      </a-layout-sider>
      <a-layout style="padding: 0 24px 24px">
        <a-layout-content
          :style="{ background: '#fff', padding: '24px', margin: 0, minHeight: '280px' }"
        >
          <posts ref="posts" />
        </a-layout-content>
      </a-layout>
    </a-layout>
  </a-layout>
</template>


<style lang="scss">
.logo {
  height: 48px;
  width: 48px;
  margin-bottom: 15px;
}

.logo-text {
  color: white;
  margin-left: 15px;
  font-size: 24px;
}

.header {
  border-bottom: 5px;
  border-color: white;
}

a-layout-slider {
  width: 200px;
}

.ant-layout {
  min-height: 93vh;
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
      countryOption: [],
    };
  },
  methods: {
    // Called when clicking on a region in the sidebar to set it as a preference.
    setPrefCookie: function (token) {
      localStorage.setItem("country", token);
      this.countryOption = [token];
      this.$refs.posts.fetchPosts();
    },
  },
  mounted() {
    //Set the default option for country to all if localStorage key doesn't exist.
    if (localStorage.getItem("country") === null) {
      localStorage.setItem("country", "all");
    }
    this.countryOption = [localStorage.getItem("country")];
  },
};
</script>
