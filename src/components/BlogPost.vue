<template>
    <div class="blogpost" v-bind:class="{ highlighted: post.highlighted }">
      <h2>{{ post.title }}</h2>
      <p>{{ post.body }}</p>
      <p class="meta">Written by {{ post.author }} on {{ date }}</p>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

export interface Post {
    title: string;
    body: string;
    author: string;
    datePosted: Date;
    highlighted?: boolean;
}

@Component
export default class BlogPost extends Vue {
  @Prop({type: Object as () => Post}) private post!: Post;

  get date() {
    return `${this.post.datePosted.getDate()}/${this.post.datePosted.getMonth()}/${this.post.datePosted.getFullYear()}`;
  }
}
</script>

<style lang="scss">
div.blogpost {
  width: 400px;
  margin: 0 auto;
  &.highlighted {
    border: 1px solid #f4d942;
    background-color: #fff3b2;
  }
  h2 {
    text-decoration: underline;
  }
  p.meta {
    font-style: italic;
  }
}
</style>
