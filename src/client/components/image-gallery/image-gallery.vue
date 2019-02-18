<template>
  <ul class="image-gallery">
    <li class="image-gallery__image" v-for="image in images" :key="image.url">
      <responsive-image :image="image" />
    </li>
  </ul>
</template>

<style>
.image-gallery {
  padding: 0;
  list-style: none;
  display: flex;
  width: var(--max-width);
  align-items: center;
  overflow: scroll;
}

.image-gallery__image {
  flex-basis: 90%;
  flex-shrink: 0;
  padding: var(--spacing-default);
}
</style>

<script>
import ResponsiveImage from '../responsive-image'

export default {
  components: { ResponsiveImage },
  props: {
    images: {
      type: Array,
      default: () => []
    }
  }
}
</script>
