<template>
  <v-content class="pa-0">

    <v-container fluid class="pt-3 mb-0 grey lighten-5">
      <v-layout wrap align-center justify-center row fill-height class="my-0">
        <v-flex xs12 md10 class="my-0">
            <p class="google-font mb-0" style="font-size:200%;color:#666;">{{ChapterDetails.ChapterName}}'s Events</p>
            <p class="google-font mt-0 mb-0" style="font-size:110%">
            We try to make our events as affordable as possible, just enough to cover our operating expenses. 
            We are able to do this by the generous support of our sponsors. If you are interested in becoming a sponsor, Please contact {{ChapterDetails.ChapterEmail}} . We would love to hear from you!</p>
        </v-flex>
      </v-layout>
    </v-container>

    <v-container fluid class="grey lighten-5">
      <v-layout wrap align-center justify-center row fill-height>
        <v-flex xs12 md10 class="">
          <upcommingEvents/>
        </v-flex>
      </v-layout>
    </v-container>

    <v-container fluid class="" >
      <v-layout wrap align-center justify-center row fill-height>
        <v-flex xs12 md10 class="">
          <pastEvents/>
        </v-flex>
      </v-layout>
    </v-container>

  </v-content>
  
</template>

<script>
import ChapterDetails from '@/assets/data/chapterDetails.json'
import upcommingEvents from '@/components/events/upcomingEvents'
import pastEvents from '@/components/events/pastEvents'
  export default {
    components: {
      upcommingEvents,
      pastEvents
    },
    data() {
      return {
        ChapterDetails: ChapterDetails
      }
    },
  }
</script>
