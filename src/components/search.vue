<template>
  <el-form
    :model="form"
    label-width="80px"
    :inline="false"
    size="normal"
    class="form"
    action="newpage"
  >
    <el-input
      v-model="keywords"
      placeholder="请输入关键字"
      clearable
    ></el-input>

    <el-checkbox-group v-model="searchCheckList" size="normal">
      <el-checkbox
        v-for="item in searchSites"
        :key="item.key"
        :label="item.label"
      >
        {{ item.text }}
      </el-checkbox>
    </el-checkbox-group>

    <el-checkbox-group v-model="repositoryCheckList" size="normal">
      <el-checkbox
        v-for="item in repositorySites"
        :key="item.key"
        :label="item.label"
      >
        {{ item.text }}
      </el-checkbox>
    </el-checkbox-group>
    
    <el-checkbox-group v-model="videoCheckList" size="normal">
      <el-checkbox
        v-for="item in videoSites"
        :key="item.key"
        :label="item.label"
      >
        {{ item.text }}
      </el-checkbox>
    </el-checkbox-group>
    
    <div>
      <span>高级搜索</span>
      <el-switch
        v-model="isExpert"
        :active-value="true"
        :inactive-value="flase"
      ></el-switch>
    </div>
    <div v-show="isExpert" class="exportsearch">
      <el-form-item label="时间范围:" size="mini">
        <el-date-picker
          v-model="date_value"
          type="daterange"
          align="right"
          unlink-panels
          range-separator="至"
          start-placeholder="开始日期"
          end-placeholder="结束日期"
          :shortcuts="shortcuts"
        >
        </el-date-picker>
      </el-form-item>
      <el-form-item label="类型:" size="mini">
        <el-select v-model="type_value" clearable placeholder="请选择">
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          >
          </el-option>
        </el-select>
      </el-form-item>
    </div>
    <el-button type="primary" size="default" @click="newpage">搜索</el-button>
  </el-form>
</template>

<script>
export default {
  name: "search",
  props: {
    searchCheckList: {
      type: Array,
      default: ["baidu"]
    },
    repositoryCheckList: {
      type: Array,
      default: []
    },
    videoCheckList: {
      type: Array,
      default: []
    }
  },
  data() {
    return {
      searchSites: [
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
      repositorySites: [
        {
          label: "Gitee",
          text: "码云",
        },
        {
          label: "Github",
          text: "Github",
        }
      ],
      videoSites: [
        {
          label: "bilibili",
          text: "哔哩哔哩",
        }
      ],
      keywords: "",
      shortcuts: [
        {
          text: "最近一天",
          value: (() => {
            const end = new Date();
            const start = new Date();
            start.setTime(start.getTime() - 3600 * 1000 * 24);
            return [start, end];
          })(),
        },
        {
          text: "最近一周",
          value: (() => {
            const end = new Date();
            const start = new Date();
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
            return [start, end];
          })(),
        },
        {
          text: "最近一个月",
          value: (() => {
            const end = new Date();
            const start = new Date();
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
            return [start, end];
          })(),
        },
        {
          text: "最近三个月",
          value: (() => {
            const end = new Date();
            const start = new Date();
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 90);
            return [start, end];
          })(),
        },
        {
          text: "最近一年",
          value: (() => {
            const end = new Date();
            const start = new Date();
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 365);
            return [start, end];
          })(),
        },
      ],
      options: [
        {
          value: "null",
          label: "不限",
        },
        {
          value: "blog",
          label: "博客",
        },
        {
          value: "quest",
          label: "问答",
        },
      ],
      isExpert: "false",
      date_value: "",
      type_value: "null",
    };
  },
  methods: {
    newpage() {
      // 高级搜索要做额外的插值
      for (const item in this.searchCheckList) {
        switch (this.searchCheckList[item]) {
          case "baidu":
            // window.close('baidu')
            window.open(
              "https://www.baidu.com/s?ie=UTF-8&wd=" + this.keywords,
              "baidu"
            );
            break;
          case "csdn":
            window.open(
              "https://so.csdn.net/so/search/all?q=" +
                this.keywords +
                "&t=all&p=1&s=0&tm=0&lv=-1&ft=0&l=&u=",
              "csdn"
            );
            break;
          case "cnblog":
            window.open(
              "https://zzk.cnblogs.com/s?w=" + this.keywords,
              "cnblog"
            );
            break;
          case "zhihu":
            window.open(
              "https://www.zhihu.com/search?type=content&q=" +
                "?wd=" +
                this.keywords,
              "zhihu"
            );
            break;
        }
      }
      for (const item in this.repositoryCheckList) {
        switch (this.repositoryCheckList[item]) {
          case "Gitee":
            window.open(
              "https://search.gitee.com/?skin=rec&type=repository&q=" +
                this.keywords +
                "&repo=&reponame=",
              "gitee"
            );
            break;
          case "Github":
            window.open(
              "https://github.com/search?q=" + this.keywords,
              "github"
            );
            break;
        }
      }
      for (const item in this.videoCheckList) {
        switch (this.videoCheckList[item]) {
          case "bilibili":
            window.open(
              "https://search.bilibili.com/all?keyword=" + this.keywords,
              "bilibili"
            );
            break;
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

.el-input__inner {
  height: 50px;
  font-size: 16px;
}
.exportsearch {
  text-align: left;
  width: 70%;
  margin: auto;
}
</style>
