<template>
  <div id="app">
    <div v-if="!repoName">loading</div>
    <div v-else>most star repo is <a :href="repoUrl">{{repoName}}</a></div>
  </div>
</template>

<script>/* eslint-disable */
export default {
  data () {
    return {
      repoUrl: '',
      repoName: ''
    }
  },
  mounted () {
    // 接口地址
    const searchUrl = 'https://api.github.com/search/repositories?q=v&sort=stars';
    // 发送ajax请求
    this.$http.get(searchUrl).then(
      response => {
        const result = response.data;
        const mostRepo = result.items[0];
        this.repoUrl = mostRepo.html_url;
        this.repoName = mostRepo.name;
      },
      response => {
        // const result=response.data;
        console.log('请求失败')
      }
    )
  }
}
</script>

<style>

</style>
