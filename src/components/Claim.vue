<template>
  <div :class="$style['claimContainer']">
    <h1 :class="$style['claim']">SPACER</h1>
    <p :class="$style['subclaim']">
      Begin your journey through our amazing galaxy,
      and discover places you never even heard of.
    </p>
    <p :class="$style['subclaim']">Type anything space-related to start.</p>
  </div>
</template>

<script>
export default {
  name: 'Claim',
};
</script>

<style module lang="scss">
.claimContainer {
  display: flex;
  text-align: center;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: white;

  .claim {
    font-size: 50px;
    margin: 0;
    @media (min-width: 768px) {
      font-size: 80px;
    }
    @media (min-width: 1024px) {
      font-size: 100px;
    }
  }
  .subclaim {
    margin: 20px 0 0 0;
    font-size: 13px;
    font-weight: 400;
    @media (min-width: 768px) {
      font-size: 17px;
      width: 500px;
      line-height: 1;
      letter-spacing: 1px;
    }
  }
}

</style>
