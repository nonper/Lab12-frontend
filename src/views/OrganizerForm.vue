<template>
  <div>
    <h1>Create an event</h1>
    <form @submit.prevent="saveEvent">
      <h3>Organizer Name</h3>

      <BaseInput v-model="event.name" type="text" label="Name" />

      <h3>The image of the event</h3>
      <UploadImages @changed="handleImages" :max="1" />

      <button type="submit">Submit</button>
    </form>

    <pre>{{ event }}</pre>
  </div>
</template>

<script>
import UploadImages from 'vue-upload-drop-images'
import OrganizerService from '../services/OrganizerService'
export default {
  inject: ['GStore'],
  components: {
    UploadImages
  },
  data() {
    return {
      event: {
        name: '',
        imageUrls: []
      },
      files: []
    }
  },
  methods: {
    saveEvent() {
      console.log(this.files)
      Promise.all(
        this.files.map((file) => {
          return OrganizerService.uploadFile(file)
        })
      ).then((res) => {
        this.event.imageUrls = res.map((r) => r.data)
        console.log(this.event.imageUrls)
        OrganizerService.saveOrganizer(this.event)
          .then((response) => {
            console.log(response)
            this.$router.push({
              name: 'OrganizerDetails',
              params: { id: response.data.id }
            })
            this.GStore.flashMessage =
              'You are succcessfully add a new organizer for ' +
              response.data.title
            setTimeout(() => {
              this.GStore.flashMessage = ''
            }, 3000)
          })
          .catch(() => {
            this.$router.push('NetworkError')
          })
      })
    },
    handleImages(files) {
      this.files = files
    }
  }
}
</script>
<style scoped></style>
