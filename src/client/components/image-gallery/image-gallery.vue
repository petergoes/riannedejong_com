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
  align-items: center;
  overflow: scroll;
}

.image-gallery__image {
  flex-basis: 95%;
  flex-shrink: 0;
  padding: var(--spacing-default);
}

.image-gallery__image:first-child {
  padding-left: 0;
}

.image-gallery__image:last-child {
  padding-right: 0;
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
