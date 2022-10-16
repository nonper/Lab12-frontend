<template>
  <h1>Events For Good</h1>

  <div class="events">
    <OrganizerCard
      v-for="event in events"
      :key="event.id"
      :event="event"
    ></OrganizerCard>
  </div>
</template>

<script>
// @ is an alias to /src
import OrganizerCard from '../components/OrganizerCard.vue'
import OrganizerService from '@/services/OrganizerService'

export default {
  name: 'EventListView',
  components: {
    OrganizerCard
  },
  data() {
    return {
      events: null
    }
  },
  // eslint-disable-next-line no-unused-vars
  beforeRouteEnter(routeTo, routeFrom, next) {
    OrganizerService.getOrganizers()
      .then((response) => {
        next((comp) => {
          comp.events = response.data
        })
      })
      .catch(() => {
        next({ name: 'NetworkError' })
      })
  }
}
</script>
<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.pagination {
  display: flex;
  width: 290px;
}

.pagination a {
  flex: 1;
  text-decoration: none;
  color: #2c3e50;
}

#page-prev {
  text-align: left;
}

#page-next {
  text-align: right;
}

.search-box {
  width: 300px;
}
</style>
