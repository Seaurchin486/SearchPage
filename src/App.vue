<template>
  <el-row>
    <el-col :span="8" :offset="8"><!-- 24等分 -->
      <search-page></search-page>
    </el-col>
  </el-row>
</template>

<script>
import SearchPage from "./components/search.vue";
export default {
  name: "App",
  components: {
    SearchPage,
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
