<template>
  <div class="search-bar">
    <span class="material-icons close" @click="closeModal">close</span>
    <input type="text" 
      id="input"
      placeholder="Search..."
      @keyup.enter="handleSearch" 
      v-model="article"
      ref="search"
    />
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
      this.$router.push({path: '/search', query: { query: this.article}});
      this.closeModal();
      this.article = '';
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

  input {
    margin-top: 30vh;
    width: 90%;
    padding: 15px 13px;
    border-radius: 8px;
    border: none;
    font-size: 1rem;

    //tablet style
    @media screen and (min-width: 768px) {
      width: 60%;
    }
    //desktop style
    @media screen and (min-width: 1024px) {
      width: 40%;
    }

    &::placeholder{
      font-family: 'Roboto', sans-serif;
      font-size: 1rem;
    }
  }
}
</style>
