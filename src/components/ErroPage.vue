<template>
  <div class="error">
    <h1>Ops, an error has occured. Try again later.</h1>
  </div>
</template>

<script>
export default {
  name: 'ErrorPage',
};
</script>

<style lang="scss" scoped>
@import '@/Functions.scss';

.error {
  h1 {
    margin-top: 15vh;
    font-size: rem(25);
    font-weight: 400;
    font-family: 'Playfair Display', 'Times New Roman', Times, serif;
    text-align: center;
  }
}
</style>
