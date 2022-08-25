<template>
  <div id="app">
    <nav>
    </nav>
    <router-view/>
  </div>
</template>

<style lang="scss">
:root{
  --bg-color: #FDFDFD;

  --white: #F8F8F8;
  --black-20: #949494;
  --black-40: #6C6C6C;
  --black-60: #444444;
  --black-80: #121221;
}

*{
  box-sizing: border-box;
  margin: 0px;
  padding: 0px;
}

body{
  background-color: var(--bg-color);
  font-family: 'Roboto', sans-serif;
}
</style>
