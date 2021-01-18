<template>
  <div v-if="event">
    <h1>Edit the event here</h1>
  </div>
</template>

<script>
export default {
  props: ['event']
}
</script>