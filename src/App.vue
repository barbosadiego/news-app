<template>
  <div id="app" :class="{ searchActive: searchActive }">
    
    <transition name="menu">
      <MenuItens v-if="isMenuActive"/>
    </transition>

    <div class="content" :class="{'is-menu-active' : isMenuActive}">

      <div class="header">
        <a href="/" class="logo">
          <img src="@/assets/logo.svg" alt="News Portal logo" />
        </a>
        <div class="icons">
          <div class="search" @click="handleSearch" v-if="!isMenuActive">
            <img src="@/assets/search.svg" />
          </div>
          <div class="menu" @click="handleMenu">
            <img src="@/assets/menu.svg" />
          </div>
        </div>
      </div>

      <transition>
        <SearchBar v-if="searchActive" @searchActive="handleSearch"/>
      </transition>

      <router-view />

      <!-- Footer -->
    </div>
  </div>
</template>

<script>
import SearchBar from '@/components/SeachModal.vue';
import MenuItens from '@/components/MenuItens.vue';

export default {
  components: {
    SearchBar,
    MenuItens,
  },
  data() {
    return {
      searchActive: false,
      isMenuActive: false,
    };
  },
  methods:{
    handleSearch(){
      this.searchActive = !this.searchActive;
    },
    handleMenu(){
      this.isMenuActive = !this.isMenuActive;
    }
  }
};
</script>

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

ul, li{
  list-style: none;
}

a{
  text-decoration: none;
}

//search modal animation
.v-enter-active,
.v-leave-active {
  transition: all 0.3s ease;
  opacity: 1;
}

.v-enter,
.v-leave-to {
  opacity: 0;
  transform: translateY(-100px);
}

//menu animation
.menu-enter-active,
.menu-leave-active {
  transition: all 0.3s ease;
  opacity: 1;
}

.menu-enter,
.menu-leave-to {
  opacity: 0;
  transform: translateX(70%);
}

#app {
  z-index: 1;
  overflow: hidden;

  .content{
    z-index: 5;
    min-height: 100vh;
    padding: 30px;
    transition: .3s ease;

    &.is-menu-active{
      transform: translateX(-70%);
    }
  }

  .header,
  .icons {
    display: flex;
  }

  .header {
    justify-content: space-between;
    align-items: center;
  }

  .icons {
    gap: 10px;
    cursor: pointer;

    & > div{
      padding: 10px;
    }
  }
}
</style>
