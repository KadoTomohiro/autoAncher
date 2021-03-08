<template>
  <p>
    <template v-for="fragment in textFragments">
      <a v-if="isUrl(fragment)" :href="fragment">{{ fragment }}</a>
      <template v-else>{{ fragment }}</template>
    </template>
  </p>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'AutoAnchor',
  props: {
    text: { type: String, default: '' },
  },
  data() {
    return {
      textFragments: [],
      urlPattern: /(https?:\/\/[\w!?\/\+\-_~=;\.,*&@#$%\(\)\'\[\]]+)/i,
    }
  },
  mounted() {
    this.text
      .split(this.urlPattern)
      .forEach((textFragment) => this.textFragments.push(textFragment))
  },
  methods: {
    isUrl(text: string): boolean {
      return this.urlPattern.test(text)
    },
  },
})
</script>

<!--<style scoped></style>-->
