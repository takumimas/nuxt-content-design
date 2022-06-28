<template>
  <div>
    <div class="post">
      <Post v-for="(item, index) in data" :key="index" :item="item.item" />
    </div>
  </div>
</template>

<script>
import Fuse from "fuse.js";
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
          content: "https://.net/search",
        },
        {
          property: "og:image",
          content: "https://.net/3.jpg",
        },
      ],
    };
  },
  data() {
    return {
      data: [],
    };
  },
  async created() {
    const query = this.$route.query.q;
    let data = await this.$content("post").fetch();
    const options = {
      threshold: 0.3,
      includeScore: true,
      keys: ["title"],
    };
    const fuse = new Fuse(data, options);
    data = fuse.search(query);
    data.sort(function (a, b) {
      return a.item.publishedAt < b.item.publishedAt ? 1 : -1;
    });
    this.data = data;
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
