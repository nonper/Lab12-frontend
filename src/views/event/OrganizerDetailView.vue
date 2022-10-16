<template>
  <div v-for="event in event.ownEvents" :key="event.id">
    <h3>Own Event id:{{ event.id }}</h3>
    <p>{{ event.title }}</p>
    <p>{{ event.description }}</p>
  </div>
  <img v-for="url in event.imageUrls" :key="url" :src="url" :alt="url" />
</template>

<script>
export default {
  props: ['id', 'event']
}
</script>

<style scoped>
img {
  border: 1px solid #ddd; /* Gray border*/
  border-radius: 4px; /* Rounded border*/
  padding: 5px; /* Some padding */
  margin: 5px; /* Some margin */
  width: 150px; /* Set a small width */
}
/* Add a hover effect (blue shadow) */
img:hover {
  box-shadow: 0 0 2px 1px rgba(0, 140, 186, 0.5);
}
</style>
