<template>
  <div id="app">
    <h1>Fantasctic Blog</h1>
    <BlogPost v-for="blogpost in blogposts" :post="blogpost" :key="blogpost.title" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import BlogPost, { Post } from "./components/BlogPost.vue";

@Component({
  components: {
    BlogPost
  }
})
export default class App extends Vue {
  private blogposts: Post[] = [
    {
      title: "My first blogpost ever!",
      body: "Lorem ipsum dolor sit amet.",
      author: "Elke",
      datePosted: new Date(2019, 1, 18)
    },
    {
      title: "Look I am blogging!",
      body: "Hurray for me, this is my second post!",
      author: "Elke",
      datePosted: new Date(2019, 1, 19),
      highlighted: true
    },
    {
      title: "Another one?!",
      body: "Another one!",
      author: "Elke",
      datePosted: new Date(2019, 1, 20)
    }
  ];
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
