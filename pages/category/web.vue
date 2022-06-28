<template>
  <div class="post">
    <Post v-for="(item, index) in data" :key="index" :item="item" />
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: "Web｜",
      meta: [
        {
          property: "og:title",
          content: "Web｜",
        },
        {
          property: "og:type",
          content: "website",
        },
        {
          property: "og:url",
          content: "https://.net/category/web/",
        },
        {
          property: "og:image",
          content: "https://.net/3.jpg",
        },
        {
          name: "twitter:card",
          content: "summary_large_image",
        },
      ],
    };
  },
  async asyncData({ $content }) {
    let data = await $content("post").fetch();
    data.sort(function (a, b) {
      return a.publishedAt < b.publishedAt ? 1 : -1;
    });
    const display_post = [];
    data.forEach((item) => {
      if (item.category.id === "category-16") {
        display_post.push(item);
      }
    });
    return {
      data: display_post,
    };
  },
};
</script>

<style lang="scss" scoped>
.post {
  width: 90vw;
  margin: auto;
  margin-top: 40px;
}
</style>