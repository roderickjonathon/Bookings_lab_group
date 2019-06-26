<template>
  <div id="app">
    <bookings-form />
    <bookings-grid :bookings='bookings'/>
  </div>
</template>

<script>
import BookingsGrid from './components/BookingsGrid.vue'
import BookingsService from '@/services/BookingsService.js'
import BookingsForm from '@/components/BookingsForm.vue'
import {eventBus}  from '@/main.js'

export default {
  name: 'app',
  data(){
    return{
      bookings: []
    }
  },

  mounted(){
    BookingsService.getBookings()
    .then(bookings => this.bookings = bookings)

    eventBus.$on('booking-added', booking =>
    this.bookings.push(booking))

    eventBus.$on('booking-deleted', id => {
      const index = this.bookings.findIndex(booking => booking._id === id)
      this.bookings.splice(index, 1)
    })

    eventBus.$on('booking-updated', booking =>{
      // const index = this.bookings.findIndex(booking => booking === booking)
      // this.bookings.splice(index, 1, booking)
    })

  },


  components: {

    'bookings-grid': BookingsGrid,
    'bookings-form': BookingsForm

  }
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    border: solid 5px;
    display: flex;
    flex-flow: column wrap;

  }
</style>
