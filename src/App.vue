<template>
  <div id="app">
    <h1>Fantasctic Blog</h1>
    <button @click="toggleHighlightedPostsVisibility">{{ showHighlighted ? 'Hide' : 'Show' }} highlighted posts</button>
    <BlogPost v-for="blogpost in visibleBlogPosts" :post="blogpost" :key="blogpost.title"/>
  </div>
</template>

<script lang="ts">
  import { Component, Vue } from "vue-property-decorator";
  import BlogPost, { Post } from "./components/BlogPost.vue";
  import { AxiosResponse } from "axios";

  @Component({
    components: {
      BlogPost
    }
  })
  export default class App extends Vue {
    public showHighlighted: boolean = true;

    private blogposts: Post[] = [];

    get visibleBlogPosts() {
      return this.blogposts.filter((post: Post) =>
        post.highlighted === undefined || post.highlighted === this.showHighlighted);
    }

    public toggleHighlightedPostsVisibility() {
      this.showHighlighted = !this.showHighlighted;
    }

    private created() {
      this.$http.get('http://localhost:3000/blogposts').then((response: AxiosResponse) => {
        this.blogposts = response.data.map((val: any) => ({
          title: val.title,
          body: val.title,
          author: val.author,
          datePosted: new Date(val.datePosted),
          highlighted: val.highlighted
        }));
      });
    }
  }

</script>

<style lang="scss">
  #app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
