 <template lang="html">
   <div id="grid">


   <div  v-for="(booking, index) in bookings" >
     {{booking.name}}
     {{booking.email}}
     {{booking.checkedIn}}


   </div>
 </div>

 </template>




 <script>
 import BookingsService from '@/services/BookingsService.js'

 export default {
   name: "bookings-grid",
   props: ['bookings'],



   mounted(){


   }
 }
 </script>






 <style lang="css" scoped>
 </style>
