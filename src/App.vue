<template>
  <div id="app">
    <nav class="nav">
      <a href="/" class="logo">
        <img src="@/assets/logo.svg" alt="News Portal logo" />
      </a>
      <div class="icons">
        <div class="search">
          <img src="@/assets/search.svg" />
        </div>
        <div class="menu">
          <img src="@/assets/menu.svg" />
        </div>
      </div>
    </nav>
    <router-view />
  </div>
</template>

<style lang="scss">
:root {
  --bg-color: #fdfdfd;

  --white: #f8f8f8;
  --black-20: #949494;
  --black-40: #6c6c6c;
  --black-60: #444444;
  --black-80: #121221;
}

* {
  box-sizing: border-box;
  margin: 0px;
  padding: 0px;
}

body {
  background-color: var(--bg-color);
  font-family: 'Roboto', sans-serif;
}

#app {
  padding: 30px;

  .nav, .icons {
    display: flex;
  }

  .nav{
    justify-content: space-between;
    align-items: center;
  }

  .icons{
    gap: 30px;
    cursor: pointer;
  }
}
</style>
