<template>
  <div class="event-list">
    <h1>Events for Good</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event"/>
    <div class="pagination">
      <router-link
        class="button"
        :to="{ name: 'EventList', query: {page: page - 1} }"
        rel="prev"
        v-if="page != 1"
        >Prev</router-link>
        
        <div v-for="a in totalEvents/2" :key="a">
        <router-link
        class="button"
        :to="{ name: 'EventList', query: {page: a = a++} }"
        rel="prev"
        
        :class="{ active: a == page, 'text-danger': hasError }"
        > {{ a }}</router-link>
        </div>

        <router-link
          class="button"
          :to="{ name: 'EventList', query: {page: page + 1} }"
          rel="next"
          v-if="hasNextPage"
        >Next</router-link>    
      </div>
  </div>
</template>

<script>
// @ is an alias to /src
import EventCard from "@/components/EventCard.vue";
import EventService from '@/services/EventService.js'
import { watchEffect } from 'vue'

export default {
  name: "EventList",
  props: ['page'],
  components: {
    EventCard
  },
  data() {
    return {
      events: null,
      totalEvents: 0,
      a: 1
    }
  },
  created() {
    watchEffect(() => {
      this.events = null
      EventService.getEvents(2, this.page)
      .then(response => {
        this.events = response.data,
        this.totalEvents = response.headers['x-total-count']
      })
      .catch(error => {
        console.log(error)
      })
    })
  },
  computed: {
    hasNextPage() {
      var totalPages = Math.ceil(this.totalEvents / 2)
      return this.page < totalPages
    }
  }
};
</script>


<style  scoped>
.event-list {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-items: center;

  width: 450px;
  max-width: 100%;
  margin: 0 auto;
}

.pagination {
  width: 100%;
  display: flex;
  align-content: center;
}

.button {
  display: block;
  flex: 1;
  padding: 20px;
  margin: 0 10px;
  cursor: pointer;
  color: #ffffff;
  border-radius: 3px;
  background-image: linear-gradient(to bottom right, #42b983, #1e9660);
  border: 1px solid rgba(0,0,0,.1);
  box-shadow: 0 0px 12px 0 rgba(0, 0, 0, 0.5);
  transition: .25s ease;
  opacity: .9;
}


.button.active,
.button:hover{
  transform: scale(1.05);
  opacity: 1;
}

</style>
