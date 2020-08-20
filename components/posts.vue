<template>
  <div>
    <a-layout-content :style="{ padding: '0 24px', minHeight: '280px' }">
      <div>
        <a-row :gutter="16">
          <a-spin :spinning="loading">
            <a-icon
              slot="indicator"
              type="loading"
              style="font-size: 128px; position:absolute; top:300px; left:50%"
              spin
            />
          </a-spin>
          <a-col :span="12" v-for="post in posts" :key="post.id">
            <a-card :title="post.data.title" :style="{ margin: '1rem 0px 0px'}">
              <template class="ant-card-actions" slot="actions">
                <span>
                  <p>{{convertTime(post.data.created_utc)}}</p>
                </span>
                <div>
                  <a-tooltip>
                    <template slot="title">Comments</template>
                    <a-icon type="message" />
                    <span class="bottom-number">{{post.data.num_comments - 1}}</span>
                  </a-tooltip>
                </div>
                <div>
                  <a-tooltip>
                    <template slot="title">Upvotes</template>
                    <a-icon type="like" />
                    <span class="bottom-number">{{post.data.score}}</span>
                  </a-tooltip>
                </div>
                <div>
                  <a :href="post.data.url" slot="extra" target="_blank">
                    <a-tooltip>
                      <template slot="title">Go to thread</template>
                      <a-icon type="logout" />
                    </a-tooltip>
                  </a>
                </div>
              </template>
            </a-card>
          </a-col>
        </a-row>
      </div>
    </a-layout-content>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: [],
      urlCA: `https://cors-anywhere.herokuapp.com/reddit.com/r/mechmarket/search.json?sort=new&q=title:("[CA-" NOT "[US-CA]")&restrict_sr=true&t=all`,
      urlUS: `https://cors-anywhere.herokuapp.com/reddit.com/r/mechmarket/search.json?sort=new&q=title:("[US")&restrict_sr=true&t=all`,
      urlEU: `https://cors-anywhere.herokuapp.com/reddit.com/r/mechmarket/search.json?sort=new&q=title:("[EU")&restrict_sr=true&t=all`,
      urlAU: `https://cors-anywhere.herokuapp.com/reddit.com/r/mechmarket/search.json?sort=new&q=title:("[AU")&restrict_sr=true&t=all`,
      url: `https://cors-anywhere.herokuapp.com/reddit.com/r/mechmarket/new.json`,
      country: "",
      loading: true,
    };
  },
  methods: {
    fetchPosts() {
      this.posts = [];
      this.loading = true;
      let requestUrl = "";
      switch (localStorage.getItem("country")) {
        case "all":
          this.requestUrl = this.url;
          break;
        case "can":
          this.requestUrl = this.urlCA;
          break;
        case "usa":
          this.requestUrl = this.urlUS;
          break;
        case "eur":
          this.requestUrl = this.urlEU;
          break;
        case "aus":
          this.requestUrl = this.urlAU;
          break;
        default:
          break;
      }
      this.$axios.$get(this.requestUrl).then((res) => {
        this.posts = this.posts.concat(res.data.children);
        this.loading = false;
      });
    },
    convertTime(time) {
      time = new Date(time * 1000);
      return this.$dateFns.formatDistanceToNow(time);
    },
  },
  mounted() {
    this.fetchPosts();
  },
};
</script>

<style lang="scss" scoped>
.bottom-number {
  margin-left: 5px;
  font-weight: bold;
}
</style>
