<template>
  <div v-if="event">
    <h1>Register the event here</h1>
  </div>
</template>

<script>
export default {
  props: ['event']
}
</script>