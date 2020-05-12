<template>
  <article>
    <div>
      <h1>{{post.fields.title}}</h1>
      <p>{{post.sys.createdAt}}</p>
      <div v-html="$md.render(post.fields.content)"></div>
    </div>
  </article>
</template>
<script>
import client from "~/plugins/contentful";
export default {
  asyncData({ params, error, payload }) {
    if (payload) return { post: payload };
    return client
      .getEntries({
        content_type: "post",
        "fields.slug": params.slug
      })
      .then(entires => {
        return { post: entires.items[0] };
      })
      .catch(e => {
        console.log(e);
      });
  },
  head() {
    return {
      title: this.post.fields.title
    };
  },
  mounted() {
    console.log(this.post);
  }
};
</script>

<style lang="scss">
</style>