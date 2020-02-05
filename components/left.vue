<template>
  <div class="ub ub-ac ub-ver ub-is NavBox">
    <img src="../assets/img/lznn18.jpg" alt="logo">
  </div>
</template>
<style scoped>
.NavBox {
  width: 180px;
  min-height: 400px;
  background: #485055;
  color: #fff;
  box-shadow: 1px 4px 7px rgb(79, 78, 80);
}
img{
  width: 60px;
  height: 70px;
  margin: 10px auto;
  box-shadow: 0 0 50px #fff;
  filter: brightness(66%) opacity(66%)
}
.item {
  line-height: 40px;
}
.NuxtLogo {
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
