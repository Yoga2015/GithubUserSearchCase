<template>
  <!-- 巨幕  搜索框 -->
  <section class="jumbotron">
    <h3 class="jumbotron-heading">
      Search Github Users
    </h3>
    <div>
      <input type="text" placeholder="输入你要搜索的名称" v-model="keyWord" />
      &nbsp;
      <button @click="SearchAI">搜索</button>
    </div>
  </section>
</template>

<script>
import axios from 'axios'
export default {
  name: 'GithubUserSearch',
  data() {
    return {
      keyWord: ''
    }
  },
  methods: {
    SearchAI() {
      axios.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(
        response => {
          console.log('请求成功了');
          // 发送方  ，请求成功后，就把请求回来的数据发给 GithubUserList组件
          this.$bus.$emit('getUsers', response.data.items)
        },
        error => {
          console.log('请求失败了', error.message);
        }
      )
    }
  }
}
</script>

<style></style>