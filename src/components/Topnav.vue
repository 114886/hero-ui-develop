<template>
  <div class="topnav" id="bar" :style="{ background: backgroundColor }">
    <router-link to="/" class="logo">
      <svg class="icon">
        <use xlink:href="#icon--SuperheroFlat2"></use>
      </svg>
    </router-link>
    <ul class="menu">
      <li>
        <router-link to="/doc">文档</router-link>
      </li>
    </ul>
    <svg v-if="toggleMenuButtonVisible" class="toggleAside" @click="toggleMenu">
      <use xlink:href="#icon-liebiao1"></use>
    </svg>
  </div>
</template>

<script lang="ts">
import { inject, onMounted, onUnmounted, reactive, ref, Ref } from "vue";
export default {
  props: {
    toggleMenuButtonVisible: {
      type: Boolean,
      default: false,
    },
  },
  setup() {
    let backgroundColor = ref("");
    let scrollTop = ref();
    const handleScroll = () => {
      scrollTop.value =
        window.pageYOffset ||
        document.documentElement.scrollTop ||
        document.body.scrollTop;

      //设置背景颜色的透明读
      if (scrollTop.value > 0) {
        backgroundColor.value = `rgba(215, 215, 214,${
          scrollTop.value / (scrollTop.value + 40)
        })`;
      } else if (scrollTop.value === 0) {
        backgroundColor.value = "transparent";
      }
    };
    onMounted(() => {
      window.addEventListener("scroll", handleScroll);
    });
    onUnmounted(() => {
      window.removeEventListener("scroll", handleScroll);
    });

    const menuVisible = inject<Ref<boolean>>("menuVisible"); // get
    const toggleMenu = () => {
      menuVisible.value = !menuVisible.value;
    };
    return {
      toggleMenu,
      backgroundColor,
      handleScroll,
    };
  },
};
</script>

<style lang="scss" scoped>
$color: #007974;

.topnav {
  color: $color;
  display: flex;
  padding: 10px 30px 0 115px;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 20;
  justify-content: center;
  align-items: center;
  text-align: center;
  > .logo {
    max-width: 6em;
    margin-right: auto;
    > svg {
      width: 56px;
      height: 56px;
    }
  }

  > .menu {
    display: flex;
    white-space: nowrap;
    flex-wrap: nowrap;

    > li {
      margin: 0 1em;
      font-size: 20px;
    }
  }

  > .toggleAside {
    width: 32px;
    height: 32px;
    position: absolute;
    left: 16px;
    top: 50%;
    transform: translateY(-50%);
    display: none;
    // background: fade-out(black, 0.9);
  }

  @media (max-width: 500px) {
    > .menu {
      display: none;
    }

    > .logo {
      margin: 0 auto;
    }

    > .toggleAside {
      display: inline-block;
    }
  }
}
@media (max-width: 500px) {
  .topnav {
    padding: 7px;
  }
}
</style>