<template>
  <b-card class="h-100"
          footer-bg-variant="white"
  >
    <h2 class="h5">{{ namespace.name }}</h2>
    <p v-if="namespace.meta.subtitle"
       class="font-weight-bold"
    >
          {{ namespace.meta.subtitle }}
    </p>
    <p v-if="namespace.meta.description">
      {{ namespace.meta.description }}
    </p>
    <span v-if="namespace.canUpdateNamespace"
          slot="footer"
    >
      <b-button :to="{ name: 'namespace.edit', params: { namespaceID: namespace.namespaceID } }" variant="light">
        <font-awesome-icon :icon="['far', 'edit']"></font-awesome-icon>
        Edit
      </b-button>
      <slot />
    </span>
  </b-card>
</template>
<script>
export default {
  props: {
    namespace: {
      type: Object,
      required: true,
    },
  },

  computed: {
    isEnabled () {
      return !!this.namespace.enabled
    },
  },
}
</script>
