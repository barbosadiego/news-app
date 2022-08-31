<template>
  <div class="not-found">
    <p>
      The page you are looking for have been moved, deleted, <br />
      or possibly never existed
    </p>
    <h1>404</h1>
  </div>
</template>

<script>
export default {
  name: 'PageNotFound',
};
</script>

<style lang="scss" scoped>
@import '@/Functions.scss';

.not-found {
  margin: 40px 0 1rem 0;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 100%;
  height: 60vh;

  h1 {
    font-size: rem(140);
    margin-top: 2rem;
  }

  p {
    font-size: rem(20);
    font-family: 'Playfair Display', 'Times New Roman', Times, serif;
  }
}
</style>
