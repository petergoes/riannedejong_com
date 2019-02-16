<template>
  <ul class="portfolio-overview">
    <li v-for="item in items" :key="item.slug">
      <nuxt-link :to="localeUrl({ name: 'portfolio-slug', params: { slug: item.slug } })">
        <responsive-image class="portfolio-overview__image" :image="squareImage(item.coverImage)" />
        {{ item.title }}
      </nuxt-link>
    </li>
  </ul>
</template>

<style>
.portfolio-overview {
  list-style: none;
  padding: 0;
}

.portfolio-overview__image {
  display: inline-block;
  width: 100px;
  height: 100px;
}
</style>

<script>
import ResponsiveImage from '../responsive-image'

export default {
  components: { ResponsiveImage },
  props: {
    items: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    squareImage(imageObj) {
      return {
        ...imageObj,
        height: imageObj.width
      }
    }
  }
}
</script>
