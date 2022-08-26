<template>
  <div class="home-page">
    <div class="hot-topics">
      <h1>hot topics</h1>
      <div class="item">
        <img src="@/assets/Rectangle 1.jpg" alt="" />
        <div class="text">
          <p class="title">
            Massa tortor nibh nulla condimentum imperdiet scelerisque...
          </p>
          <div class="info">
            <span class="publishedAt">2 Hours Agoi</span>
            <span class="source">CNN Indonesia</span>
          </div>
        </div>
        <div v-if="!isMobile" class="description">
          <p>
            <span>Nisi</span>, sagittis aliquet sit rutrum. Nunc, id vestibulum quam ornare
            adipiscing. Pellentesque sed turpis nunc gravida pharetra, sit nec
            vivamus pharetra. Velit, dui, egestas nisi, elementum mattis mauris,
            magnis. Massa tortor nibh nulla condimentum imperdiet scelerisque...
          </p>
          <a href="#">read more</a>
        </div>
      </div>
    </div>

    <div class="latest">
      <h2>latest news</h2>
      <div class="items-array">
        <div class="item">
          <img src="@/assets/Rectangle 1.jpg" alt="" />
          <h3 class="title">News Title Lorem Ipsum Dolor Sit Amet</h3>
          <div class="info">
            <span class="publishedAt">2 Hours Agoi</span>
            <span class="source">CNN Indonesia</span>
          </div>
        </div>
        <div class="item">
          <img src="@/assets/Rectangle 1.jpg" alt="" />
          <h3 class="title">News Title Lorem Ipsum Dolor Sit Amet</h3>
          <div class="info">
            <span class="publishedAt">2 Hours Agoi</span>
            <span class="source">CNN Indonesia</span>
          </div>
        </div>
        <div class="item">
          <img src="@/assets/Rectangle 1.jpg" alt="" />
          <h3 class="title">News Title Lorem Ipsum Dolor Sit Amet</h3>
          <div class="info">
            <span class="publishedAt">2 Hours Agoi</span>
            <span class="source">CNN Indonesia</span>
          </div>
        </div>
        <div class="item">
          <img src="@/assets/Rectangle 1.jpg" alt="" />
          <h3 class="title">News Title Lorem Ipsum Dolor Sit Amet</h3>
          <div class="info">
            <span class="publishedAt">2 Hours Agoi</span>
            <span class="source">CNN Indonesia</span>
          </div>
        </div>
        <div class="item">
          <img src="@/assets/Rectangle 1.jpg" alt="" />
          <h3 class="title">News Title Lorem Ipsum Dolor Sit Amet</h3>
          <div class="info">
            <span class="publishedAt">2 Hours Agoi</span>
            <span class="source">CNN Indonesia</span>
          </div>
        </div>
        <div class="item">
          <img src="@/assets/Rectangle 1.jpg" alt="" />
          <h3 class="title">News Title Lorem Ipsum Dolor Sit Amet</h3>
          <div class="info">
            <span class="publishedAt">2 Hours Agoi</span>
            <span class="source">CNN Indonesia</span>
          </div>
        </div>
        <div class="item">
          <img src="@/assets/Rectangle 1.jpg" alt="" />
          <h3 class="title">News Title Lorem Ipsum Dolor Sit Amet</h3>
          <div class="info">
            <span class="publishedAt">2 Hours Agoi</span>
            <span class="source">CNN Indonesia</span>
          </div>
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
    };
  },
  methods: {
    getWidth() {
      const width = window.innerWidth;
      width >= 1024 ? (this.isMobile = false) : (this.isMobile = true);
      console.log('width');
    },
    getDebounce(func, wait) {
      let time;
      return function () {
        clearTimeout(time);
        time = setTimeout(func, wait);
      };
    },
  },
  created() {
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
      @media screen and (min-width: 1024px) {
        grid-template-columns: repeat(4, 1fr);
      }

      .item {
        img {
          border-radius: 8px;
          margin-bottom: 8px;
        }

        .title {
          font-weight: 700;
          font-size: rem(16);
          line-height: rem(22);
          font-family: 'Playfair Display', 'Times New Roman', Times, serif;
        }

        .info {
          display: flex;
          font-size: rem(10);
          font-weight: 400;
          line-height: rem(16);
          gap: 5px;
          margin-top: 10px;
          color: var(--black-20);
        }
      }
    }
  }
}
</style>
