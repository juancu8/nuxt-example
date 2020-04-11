<template>
  <div class="container">
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>
<script>
import EventCard from '~/components/EventCard.vue'
export default {
  components: {
    EventCard
  },
  asyncData({ $axios, error }) {
    const point = 'http://localhost:3000/events'
    return $axios
      .get(point)
      .then((response) => {
        return {
          events: response.data
        }
      })
      .catch((e) => {
        error({
          statusCode: 503,
          message: 'Unable to fetch events this time. Please try again.'
        })
      })
  },
  head() {
    return {
      title: 'Event Listing'
    }
  }
}
</script>
