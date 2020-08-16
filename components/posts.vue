<template>
  <div>
    <a-layout-content :style="{ padding: '0 24px', minHeight: '280px' }">
      <div>
        <a-row :gutter="16">
          <a-col :span="12" v-for="post in posts" :key="post.id">
            <a-card :title="post.data.title" :style="{ margin: '1rem 0px 0px'}">
              <a :href="post.data.url" slot="extra" target="_blank">Go to thread</a>
              <template class="ant-card-actions" slot="actions">
                <span>
                  <p>{{convertTime(post.data.created_utc)}}</p>
                </span>
                <div>
                  <a-icon type="message" />
                  <span>{{post.data.num_comments}}</span>
                </div>
                <div>
                  <a-icon type="like" />
                  <span>{{post.data.score}}</span>
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
      url: `https://cors-anywhere.herokuapp.com/reddit.com/r/mechmarket/new.json`
    };
  },
  methods: {
    fetchPosts() {
      let requestUrl = "";
      this.$axios.$get(this.url).then(res => {
        this.posts = this.posts.concat(res.data.children);
      });
    },
    convertTime(time) {
      time = new Date(time * 1000);
      return this.$dateFns.formatDistanceToNow(time);
    }
  },
  mounted() {
    this.fetchPosts();
  }
};
</script>

<style lang="scss" scoped>
</style>
