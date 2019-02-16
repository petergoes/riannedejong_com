<template>
  <div>
    <page-layout :page="page" />

    <lazy-tracking v-if="page.hasHotjar" />
  </div>
</template>

<script>
import { LazyTracking, PageLayout } from '../components/'
import { getPageData, seoHead } from '../lib/'

export default {
  components: { LazyTracking, PageLayout },

  async asyncData ({ app }) {
    const page = await getPageData({ folder: 'pages', slug: 'home', locale: app.i18n.locale })

    return { page }
  },

  head () {
    return seoHead(this.page.seo)
  },
}
</script>
