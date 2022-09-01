<template>
  <div class="loading">
    <div class="dot item1"></div>
    <div class="dot item2"></div>
    <div class="dot item3"></div>
    <div class="dot item4"></div>
  </div>
</template>

<script>
export default {
  name: 'LoadingComponent',
};
</script>

<style lang="scss" scoped>
.loading {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: calc(100vh - 90px);
  gap: 1rem;

  .dot {
    width: 20px;
    height: 20px;
    background-color: var(--black-80);
    border-radius: 50%;
    animation: upDots 0.5s alternate infinite;
  }

  .item1 {
    animation-delay: 0.1s;
  }

  .item2 {
    animation-delay: 0.2s;
  }

  .item3 {
    animation-delay: 0.3s;
  }

  .item4 {
    animation-delay: 0.4s;
  }

  @keyframes upDots {
    from {
      transform: translate3d(0px, -30px, 0px);
    }
    to {
      transform: translate3d(0px, 0px, 0px);
    }
  }
}
</style>
