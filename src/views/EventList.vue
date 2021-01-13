<template>
  <div class="event-list">
    <h1>Events for Good</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event"/>
  </div>
</template>

<script>
// @ is an alias to /src
import EventCard from "@/components/EventCard.vue";
import EventService from '@/services/EventService.js'

export default {
  name: "EventList",
  components: {
    EventCard
  },
  data() {
    return {
      events: null
    }
  },
  created() {
    EventService.getEvents()
    .then(response => {
      this.events = response.data
    })
    .catch(error => {
      console.log(error)
    })
  }
};
</script>

<style scoped>
.event-list {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-items: center;
}

</style>
