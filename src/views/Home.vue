<template>
  <div class="home-page">
    <div class="hot-topics">
      <h1>hot topics</h1>
      <div class="item">

        <img :src="hotTopics[0].urlToImage ? hotTopics[0].urlToImage : 'https://via.placeholder.com/750'" :alt="hotTopics[0].title"/>
        <div class="text">
          <p class="title">
            {{ hotTopics[0].title }}
          </p>
          <div class="info">
            <span class="publishedAt">{{ hotTopics[0].publishedAt }}</span>
            <span class="source">{{ hotTopics[0].source.name }}</span>
          </div>
        </div>

        <div v-if="!isMobile" class="description">
          <p>
            <!-- <span>Nisi</span>, sagittis aliquet sit rutrum. Nunc, id vestibulum quam ornare
            adipiscing. Pellentesque sed turpis nunc gravida pharetra, sit nec
            vivamus pharetra. Velit, dui, egestas nisi, elementum mattis mauris,
            magnis. Massa tortor nibh nulla condimentum imperdiet scelerisque... -->
            {{ clearText(hotTopics[0].content) }}
          </p>
          <a :href="hotTopics[0].url" target="_blank">Read more</a>
        </div>

      </div>
    </div>

    <div class="latest">
      <h2>latest news</h2>
      <div class="items-array">

        <div class="item" v-for="item, index in headlines" :key="`${index} - ${item.source.name}`">
          <a :href="item.url" target="_blank" rel="noopener noreferrer">
            <img :src="item.urlToImage ? item.urlToImage : 'https://via.placeholder.com/450' " :alt="item.title" />
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
export default {
  name: 'HomePage',
  data() {
    return {
      isMobile: true,
      headlines: [],
      hotTopics: [],
    };
  },
  methods: {
    getWidth() {
      const width = window.innerWidth;
      width >= 1024 ? (this.isMobile = false) : (this.isMobile = true);
    },
    getDebounce(func, wait) {
      let time;
      return function () {
        clearTimeout(time);
        time = setTimeout(func, wait);
      };
    },
    timeLocale(time){
      return new Date(time).toLocaleDateString('pt-BR')
    },
    clearText(text){
      const regex = /\[\+\d+\s\w+\]/g
      return text.replace(regex, '')
    },
    async getHeadlines(){
      const data = await fetch('https://newsapi.org/v2/top-headlines?country=br&apiKey=10a22d9d876f43d5976a12223845ad75')
      const response = await data.json()
      this.headlines = response.articles
      // console.log(this.headlines)
    },
     async getTopNews(){
      const data = await fetch('https://newsapi.org/v2/top-headlines?sources=globo&apiKey=10a22d9d876f43d5976a12223845ad75')
      const response = await data.json()
      this.hotTopics = response.articles
      // console.log(this.hotTopics)
    },
  },
  created() {
    // this.getHeadlines()
    // this.getTopNews()
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
        // background-color: rgba($color: #000000, $alpha: .4);
        background: linear-gradient(180deg, transparent 30%, #000000);
        //desktop style
        @media screen and (min-width: 1024px) {
          grid-column: 1/4;
        }
      }

      img {
        width: 100%;
        object-fit: cover;
        //tablet style
        @media screen and (min-width: 768px) {
          height: 355px;
          border-radius: 8px;
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

      .description{
        grid-column: 4/5;
        padding: 10px 30px;
        font-size: rem(16);
        font-family: 'Playfair Display', 'Times New Roman', Times, serif;
        font-weight: 400;
        line-height: rem(32);

        span{
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
          @media screen and (min-width:768px) {
            display: flex;
            flex-wrap: wrap;
          }

          span{
            display: block;
          }
        }
      }
    }
  }
}
</style>
