<template>
  <div class="home-page">

    <div class="hot-topics">
      <h1>hot topics</h1>
      <div class="item">
        <img src="@/assets/Rectangle 1.jpg" alt="" />
        <p class="title">
          Massa tortor nibh nulla condimentum imperdiet scelerisque...
        </p>
        <span class="publishedAt">2 Hours Agoi</span>
        <span class="source">CNN Indonesia</span>
        <p v-if="!isMobile" class="description">Nisi, sagittis aliquet sit rutrum. Nunc, id vestibulum quam ornare adipiscing. Pellentesque sed turpis nunc gravida pharetra, sit nec vivamus pharetra. Velit, dui, egestas nisi, elementum mattis mauris, magnis. Massa tortor nibh nulla condimentum imperdiet scelerisque... read more</p>
      </div>
    </div>

    <div class="latest">
      <h2>latest news</h2>
      <div class="items-array">
        <div class="item">
          <img src="@/assets/Rectangle 1.jpg" alt="" />
          <h3 class="title">News Title Lorem Ipsum Dolor Sit Amet</h3>
          <span class="publishedAt">2 Hours Agoi</span>
          <span class="source">CNN Indonesia</span>
        </div>
        <div class="item">
          <img src="@/assets/Rectangle 1.jpg" alt="" />
          <h3 class="title">News Title Lorem Ipsum Dolor Sit Amet</h3>
          <span class="publishedAt">2 Hours Agoi</span>
          <span class="source">CNN Indonesia</span>
        </div>
        <div class="item">
          <img src="@/assets/Rectangle 1.jpg" alt="" />
          <h3 class="title">News Title Lorem Ipsum Dolor Sit Amet</h3>
          <span class="publishedAt">2 Hours Agoi</span>
          <span class="source">CNN Indonesia</span>
        </div>
        <div class="item">
          <img src="@/assets/Rectangle 1.jpg" alt="" />
          <h3 class="title">News Title Lorem Ipsum Dolor Sit Amet</h3>
          <span class="publishedAt">2 Hours Agoi</span>
          <span class="source">CNN Indonesia</span>
        </div>
        <div class="item">
          <img src="@/assets/Rectangle 1.jpg" alt="" />
          <h3 class="title">News Title Lorem Ipsum Dolor Sit Amet</h3>
          <span class="publishedAt">2 Hours Agoi</span>
          <span class="source">CNN Indonesia</span>
        </div>
        <div class="item">
          <img src="@/assets/Rectangle 1.jpg" alt="" />
          <h3 class="title">News Title Lorem Ipsum Dolor Sit Amet</h3>
          <span class="publishedAt">2 Hours Agoi</span>
          <span class="source">CNN Indonesia</span>
        </div>
        <div class="item">
          <img src="@/assets/Rectangle 1.jpg" alt="" />
          <h3 class="title">News Title Lorem Ipsum Dolor Sit Amet</h3>
          <span class="publishedAt">2 Hours Agoi</span>
          <span class="source">CNN Indonesia</span>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'HomePage',
  data(){
    return{
      isMobile: true,
    }
  }
};
</script>

<style lang="scss" scoped>
@import '@/Functions.scss';

.home-page{
  display: flex;
  flex-direction: column;


  .hot-topics{
    margin: 40px 0px;

    h1{
      text-transform: capitalize;
      font-size: rem(36);
      line-height: rem(43);
    }
  }

  .latest{

    .items-array{
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 32px 20px
    }
    
  }
}
</style>
