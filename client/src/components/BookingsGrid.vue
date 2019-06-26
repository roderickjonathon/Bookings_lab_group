<template lang="html">
  <div id="grid">


    <div  v-for="(booking, index) in bookings" >
      {{booking.name}}
      {{booking.email}}
      {{booking.checkedIn}}

      <button type="button" name="button" v-on:click="handleDelete(booking._id)" >Delete Booking</button>
    </div>
  </div>

</template>




<script>
import BookingsService from '@/services/BookingsService.js'
import {eventBus} from '@/main.js'

export default {
  name: "bookings-grid",
  props: ['bookings'],

  methods: {
    handleDelete(id){
      BookingsService.deleteBooking(id)
      .then(responce => eventBus.$emit('booking-deleted', id))
    }
  },

  mounted(){


  }
}
</script>






<style lang="css" scoped>
</style>
