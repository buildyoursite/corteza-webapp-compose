<script>
import base from './base'
import * as Viewers from './loader'

// Renders one of the field kind components
export default {
  components: {
    ...Viewers,
  },

  extends: base,

  computed: {
    component () {
      const kind = this.field.kind.toLocaleLowerCase()
      const keys = Object.keys(this.$options.components)
      const i = keys.map(c => c.toLocaleLowerCase()).findIndex(c => c === kind)

      if (i >= 0) {
        return this.$options.components[keys[i]]
      } else {
        return null
      }
    },
  },

  render (createElement) {
    const cmp = this.component

    if (cmp) {
      return createElement(cmp, {
        props: this.$props,
      })
    } else {
      return createElement('code', this.$t('notification.field.unknownFieldKind', { kind: this.field.kind }))
    }
  },
}
</script>
