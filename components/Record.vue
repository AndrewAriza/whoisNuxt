<template>
  <b-card
    border-variant="success"
    header-bg-variant="success"
    header-text-variant="white"
    align="center"
    header="Records"
  >
    <b-card-text>
      <b-list-group>
        <b-button-group v-for="(item, index) in records" :key="index" size="lg">
          <b-button variant="success">{{ item.sslgrade }}</b-button>
          <b-button variant="outline-secondary">{{ item.domain }}</b-button>
        </b-button-group>
      </b-list-group>
    </b-card-text>
  </b-card>
</template>

<script>
export default {
  props: {
    records: {
      type: Array,
      default: () => {
        return [
          {
            domain: '',
            sslgrade: ''
          }
        ]
      },
      required: true
    }
  }
}
</script>

<style>
.btn-group,
.btn-group-vertical {
  padding-bottom: 10px;
}
</style>
