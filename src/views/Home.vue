<template>
  <div class="home-page">
    <Loading v-if="isLoading" />

    <div>
      <div class="hot-topics">
        <h1>hot topics</h1>
        <div class="item">
          <img
            :src="
              hotTopics[newsIndex].image
                ? hotTopics[newsIndex].image
                : 'https://via.placeholder.com/750?text=Image+Not+Found'
            "
            :alt="hotTopics[newsIndex].title"
          />
          <div class="text">
            <p class="title">
              {{ hotTopics[newsIndex].title }}
            </p>
            <div class="info">
              <span class="publishedAt">{{
                hotTopics[newsIndex].publishedAt
              }}</span>
              <span class="source">{{ hotTopics[newsIndex].source.name }}</span>
            </div>
          </div>

          <div v-if="!isMobile" class="description">
            <p>
              <!-- <span>Nisi</span>, sagittis aliquet sit rutrum. Nunc, id vestibulum quam ornare
              adipiscing. Pellentesque sed turpis nunc gravida pharetra, sit nec
              vivamus pharetra. Velit, dui, egestas nisi, elementum mattis mauris,
              magnis. Massa tortor nibh nulla condimentum imperdiet scelerisque... -->
              {{ clearText(hotTopics[newsIndex].content) }}
            </p>
            <a :href="hotTopics[newsIndex].url" target="_blank">Read more</a>
          </div>
        </div>
      </div>

      <div class="latest">
        <h2>latest news</h2>
        <div class="items-array">
          <div
            class="item"
            v-for="(item, index) in headlines"
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
                <span class="publishedAt">{{
                  timeLocale(item.publishedAt)
                }}</span>
                <span class="source">{{ item.source.name }}</span>
              </div>
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Loading from '@/components/Loading.vue';

export default {
  name: 'HomePage',
  components: {
    Loading,
  },
  data() {
    return {
      isMobile: true,
      headlines: [],
      hotTopics: [],
      newsIndex: 0,
      isLoading: false,
    };
  },
  methods: {
    getWidth() {
      const width = window.innerWidth;
      width >= 1024 ? (this.isMobile = false) : (this.isMobile = true);
    },
    //debounce function
    getDebounce(func, wait) {
      let time;
      return function () {
        clearTimeout(time);
        time = setTimeout(func, wait);
      };
    },
    timeLocale(time) {
      return new Date(time).toLocaleDateString('pt-BR');
    },
    clearText(text) {
      const regex = /\[\d+\s\w+\]/g;
      return text.replace(regex, '');
    },
    async getHeadlines() {
      try {
        this.isLoading = true;
        const data = await fetch(
          'https://gnews.io/api/v4/top-headlines?token=65770b6f1d5cfb259f19aa1ee5355d87&lang=pt',
        );
        const response = await data.json();
        if (data.ok) {
          this.isLoading = false;
          this.headlines = response.articles;
        } else {
          this.isLoading = false;
          this.$emit('errorActive', response.errors[0]);
          throw new Error(response.errors);
        }
      } catch (error) {
        this.isLoading = false;
        throw new Error(error);
      }
    },
    async getTopNews() {
      const data = await fetch(
        'https://gnews.io/api/v4/top-headlines?token=65770b6f1d5cfb259f19aa1ee5355d87&lang=pt',
      );
      const response = await data.json();
      this.hotTopics = response.articles;
      this.newsIndex = Math.round(Math.random() * response.articles.length - 1);
    },
  },
  created() {
    this.getHeadlines();
    this.getTopNews();
    this.getWidth();
    window.addEventListener('resize', this.getDebounce(this.getWidth, 500));
  },
};
</script>

<style lang="scss" scoped>
@import '@/Functions.scss';

.home-page {
  display: flex;
  flex-direction: column;

  .hot-topics {
    margin: 40px 0px;

    h1 {
      text-transform: capitalize;
      font-size: rem(36);
      line-height: rem(43);
      margin-bottom: 16px;
    }

    .item {
      position: relative;
      //desktop style
      @media screen and (min-width: 1024px) {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        height: 400px;
      }
      &::before {
        content: '';
        width: 100%;
        height: 100%;
        display: block;
        position: absolute;
        border-radius: 8px;
        // background-color: rgba($color: #000000, $alpha: .6);
        background: linear-gradient(
          -90deg,
          transparent,
          rgba(0, 0, 0, 0.99) 95%
        );
        //desktop style
        @media screen and (min-width: 1024px) {
          grid-column: 1/4;
        }
      }

      img {
        width: 100%;
        object-fit: cover;
        object-position: top left;
        border-radius: 8px;
        //tablet style
        @media screen and (min-width: 768px) {
          height: 355px;
        }
        //desktop style
        @media screen and (min-width: 1024px) {
          grid-column: 1/4;
          height: 100%;
          overflow: hidden;
          height: 400px;
        }
      }

      .text {
        position: absolute;
        top: 0;
        color: var(--white);
        padding: 12px;
        height: 100%;
        display: flex;
        flex-direction: column;
        gap: 8px;
        justify-content: flex-end;
        //tablet style
        @media screen and (min-width: 768px) {
          padding: 32px;
        }
        //desktop style
        @media screen and (min-width: 1024px) {
          grid-column: 1/3;
        }

        .title {
          font-size: rem(16);
          font-weight: 700;
          line-height: rem(22);
          font-family: 'Playfair Display', 'Times New Roman', Times, serif;
          //tablet style
          @media screen and (min-width: 768px) {
            font-size: rem(24);
            line-height: rem(36);
            margin-bottom: 16px;
          }
          //desktop style
          @media screen and (min-width: 1024px) {
            font-size: rem(32);
            line-height: rem(48);
            margin-bottom: 16px;
          }
        }

        .info {
          font-size: rem(13);
          font-weight: 400;
          line-height: rem(12);
          display: flex;
          flex-wrap: wrap;
          gap: 16px;
        }
      }

      .description {
        grid-column: 4/5;
        padding: 10px 30px;
        font-size: rem(18);
        font-family: 'Playfair Display', 'Times New Roman', Times, serif;
        font-weight: 400;
        line-height: rem(32);

        span {
          font-size: rem(36);
        }
      }
    }
  }

  .latest {
    h2 {
      font-size: rem(24);
      font-weight: 700;
      line-height: rem(29);
      margin-bottom: 16px;
      text-transform: capitalize;
    }

    .items-array {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 32px 20px;
      //tablet style
      @media screen and (min-width: 768px) {
        grid-template-columns: repeat(3, 1fr);
      }
      //desktop
      @media screen and (min-width: 1024px) {
        grid-template-columns: repeat(4, 1fr);
      }

      .item {
        img {
          border-radius: 8px;
          margin-bottom: 8px;
          height: 96px;
          width: 100%;
          object-fit: cover;
          object-position: left;
          //tablet
          @media screen and (min-width: 768px) {
            height: 128px;
          }
          //desktop
          @media screen and (min-width: 1024px) {
            height: 176px;
            width: 270px;
          }
        }

        .title {
          font-weight: 700;
          font-size: rem(16);
          line-height: rem(22);
          font-family: 'Playfair Display', 'Times New Roman', Times, serif;
        }

        .info {
          font-size: rem(10);
          font-weight: 400;
          line-height: rem(16);
          gap: 5px;
          margin-top: 10px;
          color: var(--black-20);
          //tablet
          @media screen and (min-width: 768px) {
            display: flex;
            flex-wrap: wrap;
          }

          span {
            display: block;
          }
        }
      }
    }
  }
}
</style>
