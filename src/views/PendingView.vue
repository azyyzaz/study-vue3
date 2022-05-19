<template>
  <div class="pending"></div>
</template>

<script>
import { ref } from "vue";
export default {
  async setup() {
    let content = ref("内容");
    content.value = await new Promise((resolve) => {
      setTimeout(() => {
        // 3秒后修改content
        resolve("你好世界");
      }, 4500);
    });
    return { content };
  },
};
</script>

<style lang="stylus"></style>
