<template>
  <div id="app">
    <keep-alive include="home">
      <router-view></router-view>
    </keep-alive>
  </div>
</template>
<script>
export default {};
</script>

<style lang="less">
* {
  padding: 0;
  margin: 0;
}
</style>
