<template>
  <div class="page--index">
    <page-layout :page="page">
      <portfolio-overview :items="portfolioItems"/>
    </page-layout>
  </div>
</template>

<script>
import PageLayout from '../components/page-layout'
import PortfolioOverview from '../components/portfolio-overview'
import { getPageData, seoHead } from '../lib/'

export default {
  components: { PageLayout, PortfolioOverview },

  async asyncData ({ app }) {
    const pagePromise = getPageData({ folder: 'pages', slug: 'home', locale: app.i18n.locale })
    const portfolioPromise = getPageData({ folder: 'portfolio', slug: 'index', locale: app.i18n.locale })
    const [ page, portfolioItems ] = await Promise.all([ pagePromise, portfolioPromise ])
    return { page, portfolioItems }
  },

  head () {
    return seoHead(this.page.seo)
  },
}
</script>

<style>
.page--index {
  --max-width: 900px;
}
</style>
