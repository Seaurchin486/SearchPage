<template>
  <el-row :gutter="10">
    <el-col :span="8" :offset="8">
      <el-form
        :model="form"
        ref="form"
        :rules="rules"
        label-width="80px"
        :inline="false"
        size="normal"
        class="form"
      >
        <el-input
          v-model="keywords"
          placeholder=""
          size="normal"
          clearable
        ></el-input>

        <el-checkbox-group v-model="checklistA" size="normal">
          <el-checkbox
            v-for="item in sitesA"
            :key="item.key"
            :label="item.label"
          >
            {{ item.text }}
          </el-checkbox>
        </el-checkbox-group>

        <el-checkbox-group v-model="checklistB" size="normal">
          <el-checkbox
            v-for="item in sitesB"
            :key="item.key"
            :label="item.label"
          >
            {{ item.text }}
          </el-checkbox>
        </el-checkbox-group>

        <el-button type="primary" size="default" @click="newpage"
          >搜索</el-button
        >
      </el-form>
    </el-col>
  </el-row>
</template>

<script>
export default {
  name: "search",
  props: {
    checklistA: {
      type: Array,
      default: ["baidu"],
    },
    checklistB: {
      type: Array,
      default: [],
    },
  },
  data() {
    return {
      sitesA: [
        {
          label: "baidu",
          text: "百度",
        },
        {
          label: "csdn",
          text: "CSDN",
        },
        {
          label: "cnblog",
          text: "博客园",
        },
        {
          label: "zhihu",
          text: "知乎",
        },
      ],
      sitesB: [
        {
          label: "Gitee",
          text: "码云",
        },
        {
          label: "Github",
          text: "Github",
        },
      ],
      keywords: "关键字",
    };
  },
  methods: {
    newpage() {
      for (const item in this.checklistA) {
          switch (this.checklistA[item]) {
            case "baidu":
              // window.close('baidu')
              window.open("https://www.baidu.com/s?ie=UTF-8&wd=" + this.keywords, 'baidu').location;
            case "csdn":
              window.open("https://so.csdn.net/so/search/all?q=" + this.keywords + "&t=all&p=1&s=0&tm=0&lv=-1&ft=0&l=&u=", 'csdn').location;
            case "cnblog":
              window.open("https://zzk.cnblogs.com/s?w=" + this.keywords, 'cnblog').location;
            case "zhihu":
              window.open("https://www.zhihu.com/search?type=content&q=" + "?wd=" + this.keywords, 'zhihu').location;
          }
      }
      for (const item in this.checklistB) {
          switch (this.checklistB[item]) {
            case "Gitee":
              window.open("https://search.gitee.com/?skin=rec&type=repository&q=" + this.keywords + '&repo=&reponame=', 'gitee').location;
            case "Github":
              window.open("https://github.com/search?q=" + this.keywords, 'github').location;
          }
      }
    },
  },
};
</script>

<style>
.form > * {
  margin: 10px auto;
}
</style>