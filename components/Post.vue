<template>
  <div>
    <div class="card" @click="go(item.id)">
      <div class="card-content">
        <p class="title">
          {{ item.title }}
        </p>
        <p class="subtitle">{{ item.category.title }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "",
  props: ["item"],
  methods: {
    go(id) {
      this.$router.push(`/post/${id}`)
    }
  },
};
</script>

<style lang="scss" scoped>
.card {
  margin-bottom: 20px;
  .title {
    font-size: 1.3rem;
  }
  .subtitle {
    font-size: 1rem;
  }
}
</style>
