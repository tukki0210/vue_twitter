<template>
<div class="container">
  <Que que="日本で２番目に高い山は？" />
  <Ans ans="富士山" />
  <Ans ans="北岳" />
  <Ans ans="立山" />
  <Ans ans="剱岳" />
</div>

</template>

<script>
import Que from "./components/Que.vue";
import Ans from "./components/Ans.vue";

export default {
  name: "App",
  components: {
    Que,
    Ans,
  },
  // data() {
  //   return {
  //     Question: "日本で２番目に高い山は？",
  //   }
  // },
};
</script>
