<template>
  <div class="category">
      <h1>Category: {{ $route.params.id }}</h1>
      <div class="items-array">

        <div class="item" v-for="item, index in newsCategory" :key="`${index} - ${item.source.name}`">
          <a :href="item.url" target="_blank" rel="noopener noreferrer">
            <img :src="item.urlToImage ? item.urlToImage : 'https://via.placeholder.com/450'" :alt="item.title" />
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
export default {
  name: 'CategoryPage',
  data(){
    return{
      newsCategory: [],
    }
  },
  methods:{
    async getCategoryNews(){
      const data = await fetch(`https://newsapi.org/v2/top-headlines?country=br&category=${this.$route.params.id}&apiKey=10a22d9d876f43d5976a12223845ad75`);
      const response = await data.json();
      this.newsCategory = response.articles;
    },
    timeLocale(time){
      return new Date(time).toLocaleDateString('pt-BR')
    },  
  },
  created(){
    this.getCategoryNews()
    console.log(this.newsCategory)
  },
  watch:{
    '$route': 'getCategoryNews'
  }
}
</script>

<style lang="scss" scoped>
  @import '@/Functions.scss';

  .category{

    h1{
      margin: 40px 0 1rem 0;
    }

    .items-array{
      display: grid;
      grid-template-columns: 1fr;
      gap: 1rem;
      //tablet
      @media screen and (min-width:768px) {
        grid-template-columns: repeat(3,1fr);
      }
      //desktop
      @media screen and (min-width:1024px){
        grid-template-columns: repeat(4,1fr);
      }

      .item a{
        display: flex;
        flex-direction: column;
        gap: 1rem;

        img{
          height: 128px;
          object-fit: cover;
          object-position: left;
          border-radius: 8px;
          //tablet
          @media screen and (min-width:768px) {
            height: 176px;
          }
        }

        .title{
          font-family: 'Playfair Display', 'Times New Roman', Times, serif;
          font-weight: 700;
          font-size: rem(16);
        }

        .info{
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