<template>
  <div class="NavBox">
    <div class="ub ub-ac box">
      <div class="logo">
        <div class="title">lznn18</div>
      </div>
      <nav class="ub Nav">
        <div
          class="ub ub-pc item"
          :class="[active===k?'active':'']"
          @click="goto(i.link)"
          v-for="(i,k) in navList"
          :key="k"
          v-text="i.name"
        ></div>
      </nav>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    active: {
      type: Number,
      default: 0
    },
    navList: {
      type: Array,
      default() {
        return [
          {
            name: "首页",
            link: "/"
          },
          {
            name: "章节",
            link: "/list"
          },
          {
            name: "回篇",
            link: "/detail"
          },
          {
            name: "大纲",
            link: "/"
          },
          {
            name: "简介",
            link: "/"
          },
          {
            name: "书签",
            link: "/"
          },
          {
            name: "分页",
            link: "/"
          }
        ];
      }
    }
  },
  methods: {
    goto(url) {
      this.$router.push(url);
    }
  }
};
</script>
<style scoped>
.NavBox {
  padding: 0 20px 0 30px;
  background: #24292c;
}
.NavBox .box {
  height: 80px;
  max-width: 1200px;
  margin: 0 auto;
  overflow: hidden;
}
.logo {
  min-width: 80px;
}
.Nav .item {
  width: 100px;
  color: #fff;
  cursor: pointer;
}
.active {
  font-size: 18px;
  text-shadow: 0 0 8px #fff;
  box-shadow: 0 40px 20px rgb(137, 119, 238);
}
.title {
  font-weight: 300;
  font-size: 50px;
  color: #fff;
  letter-spacing: 2px;
  text-shadow: 3px 2px 5px rgb(211, 25, 195);
}
.active {
  animation: 1s appear;
}

@keyframes appear {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
</style>
