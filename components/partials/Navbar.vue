<template>
  <div v-bind:is="navComponent"></div>
</template>

<script lang="ts">
import Vue from 'vue'
import koNav from './Navbar/ko.vue'
import enNav from './Navbar/en.vue'

export default Vue.extend({
  components: {},
  mounted() {
    const locale = (this as any).$i18n.locale
      // TODO
      ; (window as any).changeLang = () => {
        window.location.href = window.location.href.replace(
          `/${locale}/`,
          locale === 'ko' ? '/en/' : '/ko/'
        )
      }
  },
  computed: {
    navComponent() {
      return (this as any).$i18n.locale === 'ko' ? koNav : enNav
    }
  }
})
</script>

<style lang="postcss">
svg.icon-external-link {
  display: initial;
  vertical-align: initial;
}
</style>
