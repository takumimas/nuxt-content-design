<template>
  <div class="root">
    <hr>
    <h2>関連記事：{{category.title}}</h2>
    <Post v-for="item in posts" :key="item.id" :item="item"/>
  </div>
</template>

<script>
export default {
  props: ["category", "postId"],
  data(){
    return {
        posts:[]
    }
  },
  async fetch() {
    const data = await this.$content("post").fetch();
    let displayPost = [];
    data.forEach((item) => {
      if (item.id !== this.postId) {
        if (item.category.id === this.category.id) {
          displayPost.push(item);
        }
      }
    });
    displayPost.sort(function (a, b) {
      return a.publishedAt < b.publishedAt ? 1 : -1;
    });
    this.posts = displayPost.slice(0,3)
  },
};
</script>
<style lang="scss" scoped>
.root {
  width: 90vw;
  margin: auto;
  margin-top: 40px;
  margin-bottom: 40px;
  h2{
    font-size: 1.1rem;
    color: black;
    margin-bottom: 20px;
  }
}
</style>