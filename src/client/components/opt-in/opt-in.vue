<template>
  <div
    v-if="!isAccepted"
    role="dialog"
    class="opt-in"
    aria-labelledby="opt-in__title"
    aria-describedby="opt-in__text"
  >
    <h2 id="opt-in__title" class="a11y-sr-only" >{{ title }}</h2>
    <div id="opt-in__text" class="opt-in__text" v-html="body"></div>
    <div class="opt-in__buttons">
      <button
        ref="agreeButton"
        class="button button--primary"
        @click="onAccept"
        v-test:optInAgreeButton
      >
        {{ $t('agree') }}
      </button>
      <button
        class="button"
        @click="onDecline"
        v-test:optInDeclineButton
      >
        {{ $t('decline') }}
      </button>
    </div>
  </div>
</template>

<script>
  import { isSupported as localStorageSupported } from '../../lib/local-storage'

  export default {
    props: {
      name: String,
      title: String,
      body: String,
    },
    data () {
      const isAccepted = (localStorageSupported)
        ? localStorage.getItem(this.name)
        : false

    return { isAccepted }
  },
  created () {
    // Emit accept event if already accepted by user
    if (this.isAccepted) {
      this.$emit('accept')
    }
  },
  mounted () {
    if (!this.isAccepted) {
      this.$refs.agreeButton.focus()
    }
  },
  methods: {
    onAccept () {
      if (localStorageSupported) {
        localStorage.setItem(this.name, true)
      }
      this.$emit('accept')
    },
    onDecline () {
      this.$emit('decline')
    },
  }
}
</script>

<style>
  @import '../app-core/variables.css';

  .opt-in {
    background-color: var(--background-color);
    padding: var(--spacing-default);
  }
  .opt-in__text {
    margin-bottom: var(--spacing-default);
  }
  .opt-in__buttons {
    margin: 0 calc( -1 * var(--spacing-half))
  }
  .opt-in__buttons > * {
    margin: 0 var(--spacing-half)
  }
</style>
