<template>
  <div>
    <page-layout :page="page"/>

    <lazy-tracking v-if="page.hasHotjar" />
  </div>
</template>

<script>
import { LazyTracking, PageLayout } from '../../components/'
import { getPageData, seoHead } from '../../lib/'
import appConfig from '../../static/data/app.json'

export default {
  components: { LazyTracking, PageLayout },

  async asyncData ({ app, params, store }) {
    const { slug } = params
    const page = await getPageData({ slug: `portfolio/${slug}`, locale: app.i18n.locale })
    store.commit('setSlugI18n', page.slugI18n)
    return { page }
  },

  head () {
    return seoHead({ ...this.page.seo, titleTemplate: `%s | ${ appConfig.title }` })
  }
}
</script>
