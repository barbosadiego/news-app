<template>
  <div id="app" :class="{ searchActive: searchActive }">
    <transition name="menu">
      <MenuItens v-if="isMenuActive" @closeMenu="handleMenu" />
    </transition>

    <div v-if="!isLoading" class="content" :class="{ 'is-menu-active': isMenuActive }">
      <div class="header">
        <a href="/news-app-repo" class="logo">
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
        <SearchBar v-if="searchActive" @searchActive="handleSearch" />
      </transition>

      <router-view @errorActive="handleError(msg)" @isLoading="handleLoading(state)"/>

      <ErrorPage v-if="isError" :errorMsg="errorMsg" />
    </div>

    <footer v-if="isDesktop" class="footer">
      <p>Copyright 2022 News Portal</p>
    </footer>
  </div>
</template>

<script>
import SearchBar from '@/components/SeachModal.vue';
import MenuItens from '@/components/MenuItens.vue';
import ErrorPage from '@/components/ErroPage.vue';

export default {
  components: {
    SearchBar,
    MenuItens,
    ErrorPage,
  },
  data() {
    return {
      searchActive: false,
      isMenuActive: false,
      isError: false,
      errorMsg: '',
      isDesktop: false,
      isLoading: false,
    };
  },
  methods: {
    handleSearch() {
      this.searchActive = !this.searchActive;
    },
    handleMenu() {
      this.isMenuActive = !this.isMenuActive;
    },
    handleError(msg) {
      this.errorMsg = msg;
      this.isError = true;
    },
    checkIsDesktop() {
      // console.log(this.isDesktop)
      return window.innerWidth >= 1024
        ? (this.isDesktop = true)
        : (this.isDesktop = false);
    },
  },
  computed: {
    //debounce
    debounce(action, wait) {
      let timeout;
      return function () {
        clearTimeout(timeout);
        timeout = setTimeout(action, wait);
      };
    },
  },
  created() {
    window.addEventListener('resize', () =>
      this.debounce(this.checkIsDesktop(), 150),
    );
  },
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

ul,
li {
  list-style: none;
}

a {
  text-decoration: none;
  color: var(--black-80);
}

img {
  max-width: 100%;
  display: block;
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
  //desktop
  @media screen and (min-width: 1024px) {
    transform: translateX(20%);
  }
}

#app {
  z-index: 1;
  display: flex;
  flex-direction: column;
  min-height: 100vh;

  .content {
    flex: 1;
    z-index: 5;
    min-height: 100vh;
    padding: 30px;
    transition: 0.3s ease;
    //desktop width
    @media screen and (min-width: 1200px) {
      max-width: 1170px;
      width: 100%;
      margin: 0 auto;
    }

    &.is-menu-active {
      transform: translateX(-70%);
      overflow-y: hidden;
      height: 100vh;
      //desktop
      @media screen and (min-width: 1024px) {
        transform: translateX(-20%);
      }
    }
  }

  &.searchActive {
    .content {
      overflow-y: hidden;
      height: 100vh;
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

    & > div {
      padding: 10px;
    }
  }

  .footer {
    background-color: var(--bg-color);
    height: 83px;
    display: flex;
    align-items: center;
    justify-content: center;

    p {
      font-family: 'Playfair Display', 'Times New Roman', Times, serif;
      color: var(--black-20);
    }
  }
}
</style>
