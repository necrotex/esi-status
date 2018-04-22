<template>
    <div class="status">

        <transition name="fade">
            <div v-if="warnings.length > 0" class="alert alert-warning" role="alert">
                <p>Following routes are degraded and requests can be slow or dropped:</p>
                <hr>
                <div class="endpoint w-100" v-for="warning of warnings" v-bind:key="warning.route">
                    <endpoint v-bind:endpoint="warning"></endpoint>
                </div>
            </div>
        </transition>

        <transition name="fade">
            <div v-if="errors.length > 0" class="alert alert-danger" role="alert">
                <p>Following routes are not reachable or very slow to respond:</p>
                <hr>
                <div class="endpoint w-100" v-for="error of errors" v-bind:key="error.route">
                    <endpoint v-bind:endpoint="error"></endpoint>
                </div>
            </div>
        </transition>

        <transition name="fade">
            <div v-if="warnings.length === 0 && errors.length === 0"
                 class="alert alert-success" role="alert">
                No errors or warnings reported!
            </div>
        </transition>
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
  }
}

</script>

<style>
    .fade-enter-active, .fade-leave-active {
        transition: opacity 1s;
    }
    .fade-enter, .fade-leave-to {
        opacity: 0;
    }
</style>
