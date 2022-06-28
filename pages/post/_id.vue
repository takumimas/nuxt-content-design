<template>
  <div class="p">
    <div class="card">
      <div class="card-image">
          <img :src="require(`~/assets/${image_id}.webp`)" />

        <div class="t">
          <div>
            <h1>{{ post.title }}</h1>
            <p>{{ post.date }}</p>
            <p @click="go()">#{{ post.category.title }}</p>
          </div>
        </div>
      </div>
      <div class="card-content">
        <div class="content" v-html="post.body"></div>
        <button class="button is-fullwidth is-info is-light" @click="copy">
          {{ copyText }}
        </button>
      </div>
    </div>
    <Same :category="post.category" :postId="post.id" />
  </div>
</template>

<script>
export default {
  layout: "post",
  data: function () {
    return {
      copyText: "URLをコピー",
    };
  },
  async asyncData({ route, $content, error }) {
    try {
      let post = await $content("post/" + route.params.id).fetch();
      let image_id = Math.floor(Math.random() * 8);
      return {
        post,
        image_id,
        post_id: route.params.id,
      };
    } catch {
      error({
        statusCode: 404,
        message: "404 Not Found",
      });
    }
  },
  head() {
    return {
      title: `${this.post.title}｜`,
      meta: [
        {
          property: "og:title",
          content: `${this.post.title}｜`,
        },
        {
          property: "og:type",
          content: "artcle",
        },
        {
          property: "og:url",
          content: `https://.net/post/${this.post_id}`,
        },
        {
          property: "og:image",
          content: `https://.net/${this.image_id}.jpg`,
        },
        {
          name: "twitter:card",
          content: "summary_large_image",
        },
      ],
    };
  },
  methods: {
    go() {
      this.$router.push(`/category/${this.post.category.link}`);
    },
    copy() {
      var str = location.href;
      var listener = function (e) {
        e.clipboardData.setData("text/plain", str);
        e.preventDefault();
        document.removeEventListener("copy", listener);
      };
      document.addEventListener("copy", listener);
      document.execCommand("copy");
      this.copyText = "コピーしました";
    },
  },
};
</script>

<style lang="scss" scoped>
.p {
  margin-top: 30px;
}
.card {
  min-height: 80vh;
  margin-bottom: 30px;
  width: 90vw;
  margin: auto;
  .card-image {
    position: relative;
  }
  img {
    height: 300px;
    width: 100%;
    object-fit: cover;
  }
  .t {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 100%;
    height: 100%;
    background-color: rgba(255, 255, 255, 0.6);
    div {
      text-align: center;
      width: 90%;
      margin: auto;
      margin-top: 80px;
    }
    h1 {
      color: black;
      font-size: 1.4rem;
      font-weight: 700;
      display: inline-block;
      text-align: left;
    }
    p {
      margin-top: 20px;
      color: black;
      font-weight: 500;
      font-size: 1.1rem;
    }
  }
  .content {
    color: black;
  }
}
</style>

<style scoped>
.content >>> h1 {
  color: black;
  font-size: 1.7rem;
  font-weight: 700;
  background-color: #e4eff9;
  padding: 15px 10px;
  border-radius: 5px;
}
.content >>> h2 {
  color: black;
  font-size: 1.4rem;
  font-weight: 700;
}
</style>