<template>
  <router-link 
    :to="{ name: 'EventDetails', params: { id: event.id } }"
    class="event-link"
    >
    <div class="event-card">
      <!-- Display Event Data -->
      <h6>@ {{ event.time }} on {{ event.date }}</h6>
      <h4> {{ event.title }} </h4>
    </div>
  </router-link>
</template>

<script>
export default {
  name: 'EventCard',
  props: {
   event: Object
  }
}
</script>

<style scoped>
.event-link{
  text-decoration: none;
  display: block;
  width: 100%;
  padding: 0 10px;
}
.event-card {
  padding: 20px;
  display: block;
  width: 100%;
  cursor: pointer;
  color: #ffffff;
  border-radius: 3px;
  background-image: linear-gradient(to bottom right, #42b983, #1e9660);
  border: 1px solid rgba(0,0,0,.1);
  box-shadow: 0 0px 12px 0 rgba(0, 0, 0, 0.5);
  margin-bottom: 18px;
  transition: .25s ease;
}
.event-card:hover {
  transform: scale(1.1) translateY(-10px);
  box-shadow: 0 10px 12px 0 rgba(0, 0, 0, 0.2);
}
</style>