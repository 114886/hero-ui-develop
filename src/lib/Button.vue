<template>
  <div :size="size">
    <button v-bind="rest">
      <slot></slot>
    </button>
  </div>
</template>

<script>
export default {
  inheritAttrs: false, //是否默认继承属性
  props:{},
  setup(props, context) {
    const { size, ...rest } = context.attrs;
    return { size, rest };
    //attrs包括继承来的东西，使用上面
    // ...rest 是一个剩余操作符，就是除了size之外的 rest可以改任何名字
  },
};
</script>

<style lang="scss" scoped>
</style>