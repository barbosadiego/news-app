<template>
  <nav class="menu">
    <h1>Menu</h1>
    <ul>
      <li><a href="" class="link">business</a></li>
      <li><a href="" class="link">entertainment</a></li>
      <li><a href="" class="link">general</a></li>
      <li><a href="" class="link">health</a></li>
      <li><a href="" class="link">science</a></li>
      <li><a href="" class="link">sports</a></li>
      <li><a href="" class="link">technology</a></li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'MenuItens',
};
</script>

<style lang="scss" scoped>
.menu {
  background-color: var(--black-80);
  position: absolute;
  top: 0;
  left: 30%;
  width: 70%;
  height: 100vh;
  color: var(--white);
  padding: 30px;

  h1 {
    margin-bottom: 2rem;
    font-weight: 700;
  }

  ul {
    display: flex;
    gap: 10px;
    flex-direction: column;
    align-items: flex-start;
    padding: 1rem 0;

    li {
      a {
        display: block;
        padding: 10px 0;
        text-transform: uppercase;
        font-family: 'Roboto', sans-serif;
        font-weight: 400;
        color: var(--white);
      }
    }
  }
}
</style>
