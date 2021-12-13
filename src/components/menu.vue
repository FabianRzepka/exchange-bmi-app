<template>
  <a class="btn btn-secondary mx-2"
      :href="href"
      @click.prevent="go">
    <slot></slot>
  </a>
</template>

<script>
import routes from '../routes'
export default {
  props: {
    href: {
      currentRoute: window.location.pathname,
      type:String,
      required: true
    }
  },
  methods: {
    go () {
      this.$root.currentRoute = this.href
      window.history.pushState(null, routes[this.href], this.href)
    }
  }
}
</script>