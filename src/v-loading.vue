<template>
  <div>
    <span v-if='status' :width="width || '1em'" :height="height || '1em'">
      <slot name='spinner'>
      </slot>
      <span>{{ message }}</span>
    </span>
    <slot v-if='!status'></slot>
  </div>
</template>
<script>
  export default {
    name: 'v-loading',
    props: ['when', 'loader', 'message', 'height', 'width'],
    computed: {
      status() {
        if (this.when) {
          return this.when;
        }
        if (this.loader) {
          return this.$vuexLoading.isLoading(this.loader);
        }
        return this.$vuexLoading.anyLoading;
      }
    }
  }
</script>