<template>
  <div v-if="GStore.organizers">
    <h1>Name: {{ GStore.organizers.name }}</h1>
    <div id="nav">
      <router-link :to="{ name: 'OrganizerDetails' }">Details</router-link> |
      <router-link :to="{ name: 'OrganizerEdit' }">Edit</router-link>
    </div>
    <router-view :event="GStore.organizers" />
  </div>
</template>
<script>
export default {
  inject: ['GStore']
}
</script>
