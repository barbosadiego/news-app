<template>
  <div class="search-results">
    <Loading v-if="isLoading"/>

    <div v-else>
      <h1>search results: {{ searchItem }}</h1>
      <div class="items-array">
        <div
          class="item"
          v-for="(item, index) in searchResults"
          :key="`${index} - ${item.source.name}`"
        >
          <a :href="item.url" target="_blank" rel="noopener noreferrer">
            <img
              :src="
                item.urlToImage
                  ? item.urlToImage
                  : 'https://via.placeholder.com/450'
              "
              :alt="item.title"
            />
            <h3 class="title">{{ item.title }}</h3>
            <div class="info">
              <span class="publishedAt">{{ timeLocale(item.publishedAt) }}</span>
              <span class="source">{{ item.source.name }}</span>
            </div>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Loading from '@/components/Loading.vue';

export default {
  name: 'SearchResults',
  components: {
    Loading,
  },
  data() {
    return {
      searchResults: [],
      searchItem: '',
      isLoading: false,
    };
  },
  methods: {
    getParams() {
      const url = new URLSearchParams(window.location.search);
      const term = url.get('query');
      this.searchItem = url.get('query');
      if (term) {
        this.getSearch(term);
      }
    },
    async getSearch(query) {
      try {
        this.isLoading = true;
        const data = await fetch(
          `https://newsapi.org/v2/everything?q=${query}&language=pt&apiKey=10a22d9d876f43d5976a12223845ad75`,
        );
        if (data.ok) {
          this.isLoading = false;
          const response = await data.json();
          this.searchResults = response.articles;
        }
      } catch (error) {
        console.log(error);
      }
    },
    timeLocale(time) {
      return new Date(time).toLocaleDateString('pt-BR');
    },
  },
  created() {
    this.getParams();
  },
  watch: {
    $route: 'getParams',
  },
};
</script>

<style lang="scss" scoped>
.search-results {
  h1 {
    margin: 40px 0 1rem 0;
    text-transform: capitalize;
  }

  .items-array {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1rem;
    //tablet
    @media screen and (min-width: 768px) {
      grid-template-columns: repeat(3, 1fr);
    }
    //desktop
    @media screen and (min-width: 1024px) {
      grid-template-columns: repeat(4, 1fr);
    }

    .item a {
      display: flex;
      flex-direction: column;
      gap: 1rem;

      img {
        height: 148px;
        object-fit: cover;
        object-position: top left;
        border-radius: 8px;
        //tablet
        @media screen and (min-width: 768px) {
          height: 176px;
        }
      }

      .title {
        font-family: 'Playfair Display', 'Times New Roman', Times, serif;
        font-weight: 700;
        font-size: rem(16);
      }

      .info {
        display: flex;
        gap: 8px;
        color: var(--black-20);
        font-size: rem(12);
        line-height: rem(14);
        font-weight: 400;
      }
    }
  }
}
</style>
