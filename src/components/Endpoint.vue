<template>
    <div class="row endpoint">
        <div class="col-1">
            <span class="badge badge-dark">{{endpoint.method}}</span>
        </div>

        <div class="col-9">
            <b>{{endpoint.route}}</b>
        </div>

        <div class="col-2">
            {{endpoint.endpoint}}
        </div>
    </div>
</template>

<script>
export default {
  name: 'Endpoint',
  props: ['endpoint']
}
</script>

<style lang="scss">
    .endpoint {
        &:hover {
            background-color: white;
        }
    }
</style>
