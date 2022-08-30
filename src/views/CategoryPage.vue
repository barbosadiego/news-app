<template>
  <div class="category">
      <h1>Category: {{ $route.params.id }}</h1>
      <div class="items-array">

        <!-- <div class="item" v-for="item, index in headlines" :key="`${index} - ${item.source.name}`">
          <a :href="item.url" target="_blank" rel="noopener noreferrer">
            <img :src="item.urlToImage ? item.urlToImage : 'https://via.placeholder.com/450' " :alt="item.title" />
            <h3 class="title">{{ item.title }}</h3>
            <div class="info">
              <span class="publishedAt">{{ timeLocale(item.publishedAt) }}</span>
              <span class="source">{{ item.source.name }}</span>
            </div>
          </a>
        </div> -->

      </div>
    </div>
</template>

<script>
export default {
  name: 'CategoryPage',
}
</script>

<style lang="scss" scoped>

</style>