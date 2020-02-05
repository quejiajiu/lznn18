<template>
  <div>
    <navs :active="2" />
    <contents>
      <left />
      <mains v-if="currentAct.title" :txt="currentAct">
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
      let i = this.arr.length + 1;
      this.$axios
        .get(`txt/${i}.txt`)
        .then(response => {
          let index = response.data.indexOf("\n");
          let title = response.data.substring(0, index);
          let content = response.data.substring(index).replace("\n", "</br>");
          let obj = {
            title,
            content
          };
          this.arr.push(obj);
          this.getfile();
        })
        .catch(response => {
          // alert("错误：" + response);
        });
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
        }
      } else if (type === "back") {
        this.currentIndex = 0;
        this.currentAct = { title: "" };
      } else {
        if (this.currentIndex !== this.arr.length - 1) {
          this.currentIndex++;
          this.currentAct = this.arr[this.currentIndex];
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
  color: midnightblue;
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
