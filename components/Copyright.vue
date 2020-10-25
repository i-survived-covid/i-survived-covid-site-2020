<template>
  <small>© 2020</small>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component
export default class Counter extends Vue {
  // data
  private year: number = 0

  // Lifecycle hook
  mounted() {
    const date = new Date();
    this.year = date.getFullYear();
  }
}
</script>
