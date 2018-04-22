<template>
    <main role="main" class="container">

        <div class="d-flex align-items-center p-3 my-3 text-white-50 header">
            <div class="lh-100">
                <h1 class="mb-0 text-white lh-100">ESI Status</h1>
                <small>Last update: {{this.lastUpdated}}</small>
            </div>

        </div>

        <Status v-if="reachable" v-bind:warnings="endpoints.warnings" v-bind:errors="endpoints.errors"></Status>
        <div v-else>
            <div class="alert alert-danger" role="alert">
                <p>ESI is not reachable.</p>
            </div>

        </div>
    </main>
</template>

<script>
import axios from 'axios'
import * as moment from 'moment'

import Status from './components/Status'

export default {
  name: 'App',
  components: {
    Status
  },

  data () {
    return {
      lastUpdated: '',
      endpoints: {
        errors: [],
        warnings: []
      },
      reachable: true
    }
  },

  methods: {
    update: function () {
      this.endpoints.errors = this.endpoints.warnings = []

      axios.get('https://esi.tech.ccp.is/status.json?version=latest').then(data => {
        this.reachable = true

        for (let endpoint of data.data) {
          if (endpoint.status === 'yellow') {
            this.endpoints.warnings.push(endpoint)
          }

          if (endpoint.status === 'red') {
            this.endpoints.errors.push(endpoint)
          }

          this.lastUpdated = moment().format('MMMM Do YYYY, HH:mm:ss')
        }
      }).catch(e => {
        this.reachable = false
      })
    }
  },

  mounted () {
    this.update()

    setInterval(() => {
      this.update()
    }, 30000)
  }
}
</script>

<style lang="scss">
    @import "~bootstrap/scss/bootstrap";
    body {
        margin: 0;
        font-family: "Roboto", "Helvetica Neue", "Helvetica", "Arial", sans-serif;
        background: #111 url(assets/background.jpg) no-repeat fixed;
        background-size: cover;
    }
    .header {
        border: 1px solid white;
        border-radius: 5px;
    }
</style>
