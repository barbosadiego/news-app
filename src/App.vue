<template>
  <div id="app" :class="{ searchActive: searchActive }">
    <transition name="menu">
      <MenuItens v-if="isMenuActive" @closeMenu="handleMenu" />
    </transition>

    <div class="content" :class="{ 'is-menu-active': isMenuActive }" >
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
        <SearchBar v-if="searchActive" @searchActive="handleSearch" />
      </transition>

      <router-view @errorActive="handleError" />

      <ErrorPage v-if="isError" :errorMsg="errorMsg"/>

      <!-- Footer -->
    </div>
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
      newsArticles: [],
      API_KEY: 'apiKey=10a22d9d876f43d5976a12223845ad75',
      country: 'country=br&',
      baseURL: 'https://newsapi.org/v2/top-headlines?',
    };
  },
  methods: {
    handleSearch() {
      this.searchActive = !this.searchActive;
      // const input = document.getElementById('input')
      // if(this.searchActive) this.$$refs.search.$el.focus()
    },
    handleMenu() {
      this.isMenuActive = !this.isMenuActive;
    },
    handleError(msg){
      this.errorMsg = msg;
      this.isError = true;
    },
    async getArticles() {
      try {
        const data = await fetch(`${this.baseURL}${this.country}${this.API_KEY}`);
        const res = await data.json();
        this.newsArticles = res.articles;
      } catch (error) {
        console.log(error, this.isError);
        this.isError = true;
      }
    },
  },
  created() {
    this.getArticles();
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

  .content {
    z-index: 5;
    min-height: 100vh;
    padding: 30px;
    transition: 0.3s ease;
    //desktop width
    @media screen and (min-width: 1200px) {
      max-width: 1170px;
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
}
</style>
