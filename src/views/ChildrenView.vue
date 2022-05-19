<template>
  <div class="children">子组件{{ mynum }}</div>
</template>

<script>
//inject API 接收父组件参数
//provide API 给子组件传递参数
import { inject } from "vue";
export default {
  setup() {
    const mynum = inject("num");
    return { mynum };
  },
};
</script>

<style></style>
