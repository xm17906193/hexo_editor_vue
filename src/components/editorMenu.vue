<template>
  <div :class="['menu-bar', hide?'hide':'']">
    <span
      :class="[item.class, active === item.class ? 'menu-active' : '']"
      v-for="(item, i) in menu"
      @click="to(item.path)"
      :key="i"
    >{{ item.name }}</span
    >
  </div>
</template>

<script>
export default {
  name: "editor-menu",
  props: ['hide'],
  data() {
    return {
      active: "",
      menu: [
        {
          name: "✨ Hexo编辑器",
          class: "hexo",
          path: "/hexo"
        },
        {
          name: "🍭 Cover>封面图",
          class: "cover",
          path: "/cover"
        },
        {
          name: "🍒 说说",
          class: "shuo",
          path: "/shuo"
        },
        {
          name: "🥕 插画&Upload",
          class: "image",
          path: "/image"
        }
      ]
    };
  },
  mounted() {
    this.activeHandle();
  },
  methods: {
    to(path) {
      this.$router.push(path);
      this.activeHandle();
    },
    activeHandle() {
      let path = this.$route.path;
      this.active = path.split("/")[1];
    }
  }
};
</script>
<style lang="scss" scoped>
.hide {
  opacity: 0 !important;
  transition: all .5s;
}

.menu-bar {
  position: absolute;
  left: 30px;
  bottom: 0;
  z-index: 99;
  opacity: 1;
  transition: all .5s;

  $bottom: 15px;

  > span {
    padding: 5px 10px 5px 10px;
    color: white;
    line-height: 10px;
    border-radius: 15px 15px 0 0;
    font-size: 12px;
    margin-right: 10px;
    position: relative;
    bottom: 5px;
    cursor: default;
    transition: all 0.2s;

    &:hover {
      transition: all 0.2s;
      padding-bottom: $bottom;
      bottom: $bottom;
    }
  }

  .menu-active {
    transition: all 0.2s;
    padding-bottom: $bottom;
    bottom: $bottom;
  }

  .hexo {
    background-color: #00caff90;
  }

  .cover {
    background-color: #FF6B6B90;
  }

  .shuo {
    background-color: #eba2e690;
  }

  .image {
    background-color: #48c08890;
  }
}
</style>
