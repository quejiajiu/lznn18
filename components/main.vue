<template>
  <div class="ub ub-ver main">
    <slot>
      <div class="ub ub-pc title" v-html="txt.title"></div>
      <div class="content" v-html="txt.content"></div>
      <div class="info" v-if="txt.info" v-html="txt.info"></div>
    </slot>
    <slot name="footer"></slot>
  </div>
</template>
<script>
export default {
  props: {
    txt: {
      type: Object,
      default() {
        return {
          title: "",
          content: "",
          info: ""
        };
      }
    }
  }
};
</script>
<style scoped>
.main {
  width: 100%;
  height: 100%;
  overflow-y: auto;
  padding: 20px 60px;
  box-sizing: border-box;
  background: -webkit-gradient(
    linear,
    left top,
    left bottom,
    color-stop(0%, #fdfffa),
    color-stop(100%, #dbe5eb)
  );
  color: rgb(43, 29, 29);
  text-indent: 2em;
  font-size: 20px;
  line-height: 40px;
}

.title {
  line-height: 40px;
  font-weight: 600;
  font-size: 22px;
}
.info {
  margin-top: 30px;
}
</style>
