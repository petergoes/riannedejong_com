<template>
  <div>
    <page-layout :page="page">
    </page-layout>

    <section class="content-section">
      <h1>Foo</h1>
    </section>
  </div>
</template>

<script>
import { PageLayout } from '../../components/'
import { getPageData, seoHead } from '../../lib/'
import appConfig from '../../static/data/app.json'

export default {
  components: { PageLayout },

  async asyncData ({ app, params, store }) {
    const { slug } = params
    const page = await getPageData({ folder: 'pages', slug: 'portfolio', locale: app.i18n.locale })
    const portfolioItems = await getPageData({ folder: 'portfolio', slug: 'index', locale: app.i18n.locale })
    store.commit('setSlugI18n', page.slugI18n)
    return { portfolioItems, page }
  },

  head () {
    return seoHead({ ...this.page.seo, titleTemplate: `%s | ${ appConfig.title }` })
  }
}
</script>
