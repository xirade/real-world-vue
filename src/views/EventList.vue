<template>
  <h1>Events for good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<script>
import EventCard from "../components/EventCard.vue";
import EventService from "@/services/EventService.js";
// @ is an alias to /src

export default {
  name: "EventList",
  components: {
    EventCard,
  },
  data() {
    return {
      events: null,
    };
  },
  created() {
    EventService.getEvents()
      .then((res) => {
        this.events = res.data;
      })
      .catch((err) => {
        console.log(err.message);
      });
  },
};
</script>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}

h1 {
  text-transform: capitalize;
}
</style>
