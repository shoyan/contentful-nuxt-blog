<template>
  <div style="background: #fff">
    <div class="wrapper">
      <h2 class="section-headline">Recent articles</h2>
      <ul class="article-list">
        <li v-for="post in posts" v-bind:key="post">
          <img style="width:320px; height:200px;" v-bind:src="post.fields.heroImage.fields.file.url"/>
          <h3>
            <nuxt-link :to="{name: 'blog-slug', params:{slug: post.fields.slug}}">{{ post.fields.title }}</nuxt-link>
          </h3>
          <small>{{ post.fields.publishDate }}</small>
          <p>{{ post.fields.description }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { createClient } from "~/plugins/contentful.js";
const client = createClient();

export default {
  // `env` is available in the context object
  asyncData({ env }) {
    return Promise.all([
      // fetch the owner of the blog
      client.getEntries({
        "sys.id": env.CTF_PERSON_ID
      }),
      // fetch all blog posts sorted by creation date
      client.getEntries({
        content_type: env.CTF_BLOG_POST_TYPE_ID,
        order: "-sys.createdAt"
      })
    ])
      .then(([entries, posts]) => {
        // return data that should be available
        // in the template
        return {
          person: entries.items[0],
          posts: posts.items
        };
      })
      .catch(console.error);
  }
};
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>

