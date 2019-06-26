<template lang="html">
  <div id="grid">


    <div id="single-booking"  v-for="(booking, index) in bookings" >
    <h2>  Name: {{booking.name}} </h2>
    <p>  Email: {{booking.email}} </p>

      <label for="checkbox">Checked in:</label>
      <input type="checkbox" name="checkbox" :checked="booking.checkedIn" v-model='booking.checkedIn' @change="handleChange(booking)">
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

#grid {
  border: solid 3px;
  border-radius: 15px;
  padding: 2vh;
  margin: 2vh;
  flex-flow: row wrap;
}

#single-booking {
  flex-flow: row wrap;
  border: solid 3px;
  border-color: #1be;

}

</style>
