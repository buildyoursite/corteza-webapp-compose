<template>
  <b-button v-if="list.length > 0" variant="link" @click="jsonExport(list, type)">
    <font-awesome-icon :icon="['fas', 'cloud-download-alt']"></font-awesome-icon>
    {{ $t('general.label.export') }}
  </b-button>
</template>

<script>
import { saveAs } from 'file-saver'
import { mapActions } from 'vuex'

export default {
  props: {
    list: {
      type: Array,
      required: true,
    },
    type: {
      type: String,
      required: true,
    },
  },

  methods: {
    ...mapActions({
      findModuleByID: 'module/findByID',
    }),

    jsonExport (list, type) {
      Promise.all(list.map(i => i.export(this.findModuleByID))).then(list => {
        const blob = new Blob([JSON.stringify({ type, list }, null, 2)], { type: 'application/json' })
        saveAs(blob, `${type}-export.json`)
      })
    },
  },
}
</script>
