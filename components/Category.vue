<template>
  <div class="b">
    <button class="button is-rounded" :class="{'is-info':selected=='index'}" @click="go('/')">All</button>
    <button class="button is-rounded" :class="{'is-info':selected=='category-web'}" @click="go('/category/web/')">Web</button>
    <button class="button is-rounded" :class="{'is-info':selected=='category-vue_nuxt'}" @click="go('/category/vue_nuxt/')">Vue.js/Nuxt.js</button>
    <button class="button is-rounded" :class="{'is-info':selected=='category-python'}" @click="go('/category/python/')">Python</button>
    <button class="button is-rounded" :class="{'is-info':selected=='category-nodejs'}" @click="go('/category/nodejs/')">Node.js</button>
    <button class="button is-rounded" :class="{'is-info':selected=='category-diary'}" @click="go('/category/diary/')">日記</button>
    <input type="text" class="input" placeholder="検索" @keydown.enter="search" />
  </div>
</template>

<script>
export default {
  data(){
    return{
      selected:"",
    }
  },
  created:function(){
    this.selected = this.$route.name
  },
  methods:{
    go(url){
      this.$router.push(url)
    },
    search(e){
      location.href = `/search/?q=${e.target.value}`
    }
  },
  watch:{
    $route(to){
      this.selected = this.$route.name
    }
  }
}
</script>

<style lang="scss" scoped>
.b {
  width: 90vw;
  margin: auto;
  margin-top: 30px;
  button {
    margin: 5px;
    margin-left: 0;
  }
  input {
    margin: 5px;
    width: 200px;
    margin-left: 0;
  }
}
</style>