<template lang="pug">
  v-footer.justify-center(:color='bgColor', inset)
    .caption.grey--text(:class='$vuetify.theme.dark ? `text--lighten-1` : `text--darken-1`')
      // template(v-if='footerOverride')
      //   span(v-html='footerOverrideRender + ` |&nbsp;`')
      // template(v-else-if='company && company.length > 0 && contentLicense !== ``')
      //   span(v-if='contentLicense === `alr`') {{ $t('common:footer.copyright', { company: company, year: currentYear, interpolation: { escapeValue: false } }) }} |&nbsp;
      //   span(v-else) {{ $t('common:footer.license', { company: company, license: $t('common:license.' + contentLicense), interpolation: { escapeValue: false } }) }} |&nbsp;
      // span {{ $t('common:footer.poweredBy') }} #[a(href='https://wiki.js.org', ref='nofollow') Wiki.js]
      span 版权所有: ©紫光云技术有限公司 2023 版权所有     津 ICP 备 19004759号-1 
      img(src="https://www.unicloud.com/upload/images/2020/12/56b7b7d3b104eb04.png")
      span 津公网安备 12019202000336号 | 
      span {{ $t('common:footer.poweredBy') }} #[a(href='https://www.unicloud.com', ref='nofollow') Unicloud]
</template>

<script>
import { get } from 'vuex-pathify'
import MarkdownIt from 'markdown-it'

const md = new MarkdownIt({
  html: false,
  breaks: false,
  linkify: true
})

export default {
  props: {
    color: {
      type: String,
      default: 'grey lighten-3'
    },
    darkColor: {
      type: String,
      default: 'grey darken-3'
    }
  },
  data() {
    return {
      currentYear: (new Date()).getFullYear()
    }
  },
  computed: {
    company: get('site/company'),
    contentLicense: get('site/contentLicense'),
    footerOverride: get('site/footerOverride'),
    footerOverrideRender () {
      if (!this.footerOverride) { return '' }
      return md.renderInline(this.footerOverride)
    },
    bgColor() {
      if (!this.$vuetify.theme.dark) {
        return this.color
      } else {
        return this.darkColor
      }
    }
  }
}
</script>

<style lang="scss">
  .v-footer {
    a {
      text-decoration: none;
    }

    &.altbg {
      background: mc('theme', 'primary');

      span {
        color: mc('blue', '300');
      }

      a {
        color: mc('blue', '200');
      }
    }
  }
</style>
