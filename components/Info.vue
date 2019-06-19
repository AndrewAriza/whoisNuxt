<template>
  <b-card
    border-variant="success"
    header-bg-variant="success"
    header-text-variant="white"
    align="center"
    :header="domain"
  >
    <b-card-text>{{ info | pretty }}</b-card-text>
  </b-card>
</template>

<script>
export default {
  filters: {
    pretty: value => {
      return JSON.stringify(value, null, 2)
    }
  },
  props: {
    domain: {
      type: String,
      default: ''
    },
    info: {
      type: Object,
      default: () => {
        return {}
      }
    }
  }
}
</script>
