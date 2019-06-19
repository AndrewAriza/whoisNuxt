<template>
  <b-card
    border-variant="success"
    header-bg-variant="success"
    header-text-variant="white"
    :header="domain | capitalize"
  >
    <b-card-text>
      <pre>{{ info | pretty }}</pre>
    </b-card-text>
  </b-card>
</template>

<script>
export default {
  filters: {
    pretty: value => {
      return JSON.stringify(value, null, 2)
    },
    capitalize: text => {
      return text.charAt(0).toUpperCase() + text.slice(1)
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

<style>
.card-header {
  text-align: center;
}
</style>
