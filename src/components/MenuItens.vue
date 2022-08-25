<template>
  <nav class="menu">
    <ul>
      <li><a href="" class="link">item 1</a></li>
      <li><a href="" class="link">item 2</a></li>
      <li><a href="" class="link">item 3</a></li>
      <li><a href="" class="link">item 4</a></li>
      <li><a href="" class="link">item 5</a></li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'MenuItens',
}
</script>

<style lang="scss" scoped>
.menu{

  ul{
    background-color: var(--black-80);
    position: absolute;
    top: 0;
    left: 30%;
    width: 70%;
    height: 100vh;
    display: flex;
    gap: 10px;
    flex-direction: column;
    align-items: flex-start;
    padding: 1rem;

    li{
      a{
        display: block;
        padding: 10px;
        text-transform: uppercase;
        font-family: 'Roboto', sans-serif;
      }
    }
  }
}
</style>