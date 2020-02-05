<template>
  <div>
    <navs />
    <contents>
      <left />
      <mains :txt="txt" />
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
      txt: {}
    };
  },
  async asyncData({ $axios }) {
    // let res = await $axios.get(`../json/info.txt`);
    // console.log( $axios.get,1111 );
  },
  mounted() {
    this.$axios
      .get("../txt/info.txt")
      .then(response => {
        console.log(response);
        this.txt = {
          title: "简介",
          content: response.data.replace("\n", "</br>")
        };
      })
      .catch(response => {
        alert("错误：" + response);
      });
  }
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
