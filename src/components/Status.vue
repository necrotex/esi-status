<template>
    <div class="status">

        <div v-if="warnings.length > 0" class="alert alert-warning" role="alert">
            <p>Following routes are degraded and requests can be slow or dropped:</p>
            <hr>
            <div class="endpoint w-100" v-for="warning of warnings" v-bind:key="warning.endpoint">
                <endpoint v-bind:endpoint="warning"></endpoint>
            </div>
        </div>

        <div v-if="errors.length > 0" class="alert alert-danger" role="alert">
            <p>Following routes can be not reachable or very slow to respond:</p>
            <hr>
            <div class="endpoint w-100" v-for="error of errors" v-bind:key="error.endpoint">
                <endpoint v-bind:endpoint="error"></endpoint>
            </div>
        </div>

        <div v-if="warnings.length === 0 && errors.length === 0"
             class="alert alert-success" role="alert">
            Everything is alright, all routes are reachable!
        </div>
    </div>
</template>

<script>
import Endpoint from './Endpoint'

export default {
  name: 'Status',
  components: {Endpoint},
  props: {
    errors: {
      default: []
    },
    warnings: {
      default: []
    }
  },
  data: function () {
    return {}
  }

}

</script>
