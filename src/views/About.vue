<template>
  <div :class="$style['about']">
    <h1>Creeated by K.Sz. based on <a href="https://www.youtube.com/watch?v=A2rEhxkFPDw" target="blank">this course</a></h1>
  </div>
</template>

<script>
export default {
  name: 'About',
};
</script>

<style module lang="scss">
  .about {
    height: 100vh;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
