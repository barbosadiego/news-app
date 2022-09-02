<template>
  <div class="category">
    <Loading v-if="isLoading" />

    <h1>Category: {{ $route.params.id }}</h1>
    <div class="items-array">
      <div
        class="item"
        v-for="(item, index) in newsCategory"
        :key="`${index} - ${item.source.name}`"
      >
        <a :href="item.url" target="_blank" rel="noopener noreferrer">
          <img
            :src="
              item.image
                ? item.image
                : 'https://via.placeholder.com/450?text=Image+Not+Found'
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
</template>

<script>
import Loading from '@/components/Loading.vue';

export default {
  name: 'CategoryPage',
  components: {
    Loading,
  },
  data() {
    return {
      newsCategory: [],
      isLoading: false,
    };
  },
  methods: {
    handleError(msg) {
      this.$emit('errorActive', msg);
    },
    async getCategoryNews() {
      try {
        this.isLoading = true;
        const data = await fetch(
          `https://gnews.io/api/v4/search?q=${this.$route.params.id}&token=65770b6f1d5cfb259f19aa1ee5355d87&lang=pt`,
        );
        const response = await data.json();
        if (data.ok) {
          this.isLoading = false;
          this.newsCategory = response.articles;
        } else {
          this.isLoading = false;
          console.log(response);
          this.handleError(response.message);
          throw new Error(response.code + ' | ' + response.message);
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
    this.getCategoryNews();
  },
  watch: {
    $route: 'getCategoryNews',
  },
};
</script>

<style lang="scss" scoped>
@import '@/Functions.scss';

.category {
  h1 {
    margin: 40px 0 1rem 0;
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
