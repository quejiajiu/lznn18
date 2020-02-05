<template>
  <div>
    <navs :active="1" />
    <contents>
      <left />
      <mains v-if="currentAct.title" :txt="currentAct" ref="main">
        <div class="ub ub-pa footer" slot="footer">
          <div class="pre" :class="[currentIndex===0?'disable':'']" @click="footerAction('pre')">上一章</div>
          <div class="back" @click="footerAction('back')">返回列表</div>
          <div
            class="next"
            :class="[currentIndex===arr.length-1?'disable':'']"
            @click="footerAction('next')"
          >下一章</div>
        </div>
      </mains>
      <mains v-else>
        <div class="list">
          <div class="ub act" v-for="(i,k) in arr" :key="k" v-html="i.title" @click="look(i,k)"></div>
        </div>
      </mains>
    </contents>
  </div>
</template>

<script>
import navs from "~/components/nav.vue";
import left from "~/components/left.vue";
import mains from "~/components/main.vue";
import contents from "~/components/content.vue";

export default {
  components: {
    navs,
    left,
    mains,
    contents
  },
  data() {
    return {
      arr: [],
      currentAct: {
        title: "",
        content: ""
      },
      currentIndex: 0
    };
  },
  mounted() {
    this.getfile();
  },
  methods: {
    getfile() {
      let i = this.arr.length;
      try {
        let a = require(`../static/json/${i + 1}.json`);
        this.arr.push(a);
        this.getfile();
      } catch (err) {
        console.log(err);
      }
    },
    look(data, index) {
      this.currentAct = data;
      this.currentIndex = index;
    },
    footerAction(type) {
      if (type === "pre") {
        if (this.currentIndex !== 0) {
          this.currentIndex--;
          this.currentAct = this.arr[this.currentIndex];
          this.$refs.main.$el.scrollTop = 0;
        }
      } else if (type === "back") {
        this.currentIndex = 0;
        this.currentAct = { title: "" };
      } else {
        if (this.currentIndex !== this.arr.length - 1) {
          this.currentIndex++;
          this.currentAct = this.arr[this.currentIndex];
          this.$refs.main.$el.scrollTop = 0;
        }
      }
    }
  }
};
</script>

<style scoped>
.act {
  width: 33.33%;
  float: left;
  line-height: 30px;
  color: indigo;
  text-shadow: 1px 1px 3px #fff;
  cursor: pointer;
}
.footer {
  margin-top: 40px;
  color: rgb(3, 6, 179);
}
.footer > div {
  cursor: pointer;
}
.footer .disable {
  color: gray;
  cursor: no-drop;
}
</style>
