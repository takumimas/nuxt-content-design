<template>
  <div>
    <div class="post">
      <Post v-for="(item, index) in data" :key="index" :item="item" />
    </div>
  </div>
</template>

<script>
export default {
  name: "",
  head() {
    return {
      title: "",
      meta: [
        {
          property: "og:title",
          content: "",
        },
        {
          property: "og:type",
          content: "website",
        },
        {
          property: "og:url",
          content: "https://.net/",
        },
        {
          property: "og:image",
          content: "https://.net/3.jpg",
        },
        {
          name:"twitter:card",
          content:"summary_large_image"
        }
      ],
    };
  },
  async asyncData({ $content }) {
    let data = await $content("post").fetch();
    data.sort(function (a, b) {
      return a.publishedAt < b.publishedAt ? 1 : -1;
    });
    return {
      data,
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
