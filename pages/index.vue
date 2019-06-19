<template>
  <b-container class="panel">
    <b-row align-h="center">
      <logo />
    </b-row>
    <b-row align-h="center">
      <h1 class="title">
        whoisNuxt
      </h1>
    </b-row>
    <b-row align-h="center">
      <h2 class="subtitle">
        Truora Challenge
      </h2>
    </b-row>
    <b-row align-h="center">
      <b-col cols="9">
        <b-input-group>
          <b-form-input
            id="input-live"
            v-model="domain"
            :state="domainValidation()"
            aria-describedby="input-live-help input-live-feedback"
            placeholder="Enter your domain"
            trim
            :formatter="format"
            :disabled="loading"
            @keyup.enter="search"
          >
          </b-form-input>
          <b-input-group-append>
            <b-button
              variant="outline-success"
              :disabled="loading"
              @click="search"
            >
              <div v-if="loading">
                <b-spinner small type="grow"></b-spinner>
                Loading...
              </div>
              <div v-else>
                Search
              </div>
            </b-button>
          </b-input-group-append>
        </b-input-group>
      </b-col>
    </b-row>
    <b-row class="panel">
      <b-col sm="7">
        <info v-if="info" :domain="domain" :info="info" />
      </b-col>
      <b-col sm="5">
        <record v-if="records" :domain="domain" :records="records.items" />
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import Logo from '~/components/Logo.vue'
import Info from '~/components/Info.vue'
import Record from '~/components/Record.vue'

export default {
  components: {
    Logo,
    Info,
    Record
  },
  data() {
    return {
      status: false,
      domain: '',
      loading: false,
      info: null,
      records: null
    }
  },
  methods: {
    format(value, event) {
      return value.toLowerCase()
    },
    domainValidation() {
      const regex = /^(?!:\/\/)([a-zA-Z0-9-_]+\.)*[a-zA-Z0-9][a-zA-Z0-9-_]+\.[a-zA-Z]{2,11}?$/gi
      this.status = regex.test(this.domain)
      return this.domain.length === 0 || this.status
    },
    async search() {
      if (this.status) {
        this.loading = true
        this.info = await this.$axios.$get('/' + this.domain)
        this.records = await this.$axios.$get()
      }
      this.loading = false
    }
  }
}
</script>

<style>
.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 9vw;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 4vw;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.panel {
  padding-top: 15px;
}
</style>
