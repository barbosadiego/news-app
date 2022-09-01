<template>
  <div class="search-bar">
    <span class="material-icons close" @click="closeModal">close</span>
    <div class="input-area">
      <input type="text"
        id="input"
        placeholder="Search..."
        @keyup.enter="handleSearch"
        v-model="article"
        ref="search"
      />
      <button class="submit-btn" type="submit" @click="handleSearch">Go</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  data(){
    return{
      article: '',
    }
  },
  methods: {
    handleSearch() {
      if(this.article.length){
        this.$router.push({path: '/search', query: { query: this.article}});
        this.closeModal();
        this.article = '';
      }
    },
    closeModal(){
      this.$emit('searchActive')
    }
  },
};
</script>

<style lang="scss" scoped>
.search-bar {
  position: fixed;
  width: 100%;
  min-height: 100vh;
  top: 0px;
  left: 0px;
  bottom: 0px;
  z-index: 10;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  background-color: rgba($color: #000000, $alpha: .95);

  .close{
    color: var(--white);
    font-size: 2.5rem;
    position: absolute;
    right: 30px;
    top: 30px;
    cursor: pointer;
  }

  .input-area{
    margin-top: 30vh;
    display: flex;
    position: relative;
    justify-content: center;
    align-items: center;
    width: 90%;
    //tablet style
    @media screen and (min-width: 768px) {
      width: 60%;
    }
    //desktop style
    @media screen and (min-width: 1024px) {
      width: 40%;
    }

    #input {
      width: 100%;
      padding: 15px 53px 15px 13px;
      border-radius: 8px;
      border: 1px solid black;
      font-size: 1rem;
      outline: 2px solid transparent;
      transition: .3s;

      &::placeholder{
        font-family: 'Roboto', sans-serif;
        font-size: 1rem;
      }

      &:focus{
        outline: 2px solid var(--white);
      }
    }

    .submit-btn{
      position: absolute;
      height: 100%;
      width: 41px;
      right: 0px;
      cursor: pointer;
      border: none;
      background-color: var(--black-80);
      color: var(--white);
      border-radius: 0px 8px 8px 0px;
      font-size: 1rem;
    }
  }
}
</style>
