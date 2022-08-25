<template>
  <div id="app" :class="{ searchActive: searchActive }">
    <nav class="nav">
      <a href="/" class="logo">
        <img src="@/assets/logo.svg" alt="News Portal logo" />
      </a>
      <div class="icons">
        <div class="search">
          <img src="@/assets/search.svg" @click="handleSearch" />
        </div>
        <div class="menu">
          <img src="@/assets/menu.svg" />
        </div>
      </div>
    </nav>

    <transition>
      <SearchBar v-if="searchActive" @searchActive="handleSearch"/>
    </transition>

    <router-view />

    <!-- Footer -->
  </div>
</template>

<script>
import SearchBar from '@/components/SeachModal.vue';

export default {
  components: {
    SearchBar,
  },
  data() {
    return {
      searchActive: false,
    };
  },
  methods:{
    handleSearch(){
      this.searchActive = !this.searchActive
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

#app {
  padding: 30px;
  min-height: 100vh;

  .nav,
  .icons {
    display: flex;
  }

  .nav {
    justify-content: space-between;
    align-items: center;
  }

  .icons {
    gap: 30px;
    cursor: pointer;
  }
}
</style>
