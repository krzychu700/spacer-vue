<template>
  <div :style="style" :class="[$style.item]" />
</template>

<script>
export default {
  name: 'Item',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: this.item.links[0].href,
      title: this.item.data[0].title,
    };
  },
  computed: {
    style() {
      return `background-image: url("${this.photo}")`;
    },
  },
  mounted() {
    console.log(this.item);
  },
};
</script>
<style module lang="scss">
  .item {
    width: 40vw;
    height: 250px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 50%;
    @media (min-width: 768px) {
      width: 25vw;
    }
  }
</style>
