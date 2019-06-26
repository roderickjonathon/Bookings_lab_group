<template lang="html">
  <div id="grid">


    <div  v-for="(booking, index) in bookings" >
      {{booking.name}}
      {{booking.email}}

      <input type="checkbox" name="" :checked="booking.checkedIn" v-model='booking.checkedIn' @change="handleChange(booking)">
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
  data(){
    return{
      name: "",
      email: "",
      checkedIn: false
    }
  },

  methods: {
    handleDelete(id){
      BookingsService.deleteBooking(id)
      .then(response => eventBus.$emit('booking-deleted', id))
    },
    handleChange(booking){
      BookingsService.updateBooking(booking)
      .then(response => eventBus.$emit('booking-updated', booking))
    }
  },

  mounted(){


  }
}
</script>






<style lang="css" scoped>
</style>
