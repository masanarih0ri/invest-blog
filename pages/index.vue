<template>
  <div class="posts">
    <nuxt-link
      :to="`posts/${post.fields.slug}`"
      class="post"
      v-for="(post, index) in posts"
      :key="index"
    >
      <div class="thumbnail">
        <img :src="post.fields.image.fields.file.url" />
      </div>
      <div>
        <p>{{post.sys.createdAt}}</p>
        <h2>{{post.fields.title}}</h2>
      </div>
    </nuxt-link>
  </div>
</template>

<script>
import client from "~/plugins/contentful";
export default {
  asyncData({ params }) {
    return client
      .getEntries({
        content_type: "post",
        order: "-sys.createdAt"
      })
      .then(entries => {
        return { posts: entries.items };
      })
      .catch(e => {
        console.log(e);
      });
  }
};
</script>

<style>
</style>
