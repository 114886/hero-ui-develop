<template>
  <div>Button示例</div>
  <h1>示例1</h1>
  <div>
    <Button @click="onClick" @mousemove="onClick" @focus="onClick">你好</Button>
  </div>
</template>

<script lang="ts">
import Button from "../lib/Button.vue";
export default {
  components: { Button },
  setup() {
    const onClick = () => {
      console.log(1);
    };
    return { onClick };
  },
};
</script>

<style lang="scss" scoped>
</style>