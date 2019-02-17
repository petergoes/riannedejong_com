<template>
  <ul>
    <li v-for="image in images" :key="image.url">
      <responsive-image :image="image" />
    </li>
  </ul>
</template>

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
