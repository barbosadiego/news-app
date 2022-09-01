<template>
  <div class="error">
    <h1>Ops, an error has occured. Try again later.</h1>
    <p v-if="errorMsg">{{ errorMsg }}</p>
  </div>
</template>

<script>
export default {
  name: 'ErrorPage',
  props: {
    errorMsg: String,
  }
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

  p{
    font-family: 'Roboto', sans-serif;
    text-align: center;
    margin: 2rem auto;
    max-width: 60ch;
    line-height: 1.4;
  }
}
</style>
