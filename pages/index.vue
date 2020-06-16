<template>
  <div>
    <p>Hello World</p>
    some new content
    <nuxt-link :to="{ name: 'Create' }">Create Page</nuxt-link>
  </div>
</template>

<script>
export default {
  name: 'Index'
}
</script>

<style></style>
