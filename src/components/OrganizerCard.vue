<template>
  <router-link
    class="event-link"
    :to="{ name: 'OrganizerLayout', params: { id: event.id } }"
  >
    <div class="event-card">
      <span v-for="event in event.ownEvents" :key="event.id">{{
        event.title
      }}</span>
      <h5>by</h5>
      <h5>{{ event.name }}</h5>
    </div>
  </router-link>
</template>
<script>
export default {
  name: 'OrganizerCard',
  props: {
    event: {
      type: Object,
      required: true
    }
  }
}
</script>
<style scoped>
.event-card {
  padding: 20px;
  width: 250px;
  cursor: pointer;
  border: 1px solid #39495c;
  margin-bottom: 18px;
}

.event-card:hover {
  transform: scale(1.01);
  box-shadow: 0 3px 12px 0 rgba(0, 0, 0, 0.2);
}

.event-link {
  color: #2c3e50;
  text-decoration: none;
}
</style>
