<template>
  <div class="index">
    <img class="home-img" :src="$store.state.meta.projectImg" alt="homeImg" />
  </div>
</template>

<script>
export default {
  data() {
    return {}
  },
  methods: {}
}
</script>
<style lang="less">
.index {
  .home-img {
    width: 200px;
    height: 200px;
  }
}
</style>
