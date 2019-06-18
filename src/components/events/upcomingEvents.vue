<template :style="{'background-image':'url('+require('@/assets/img/svg/bg.svg')+')'}" style="background-position:right">
    <v-container class="pa-0 ">

        <v-layout wrap align-center justify-center row fill-height class="mt-0 mb-0" >
           <v-flex xs12 md12 lg12 class="pa-2 mb-0">
               <p class="google-font mb-0" style="font-size:170%;color:#0277bd">Our Feature Event & Meetup</p>     
            </v-flex> 
        </v-layout>

        <v-layout  wrap align-center justify-center row fill-height class="mt-2 elevation-2 white" style="border:1px solid #e0e0e0;border-radius:5px;margin-bottom: 30px;"  v-if="eventDetails.IsReady">
             <v-flex xs12 v-if="showLoader">
                <v-progress-circular
                     :size="50"
                     color="blue"
                     indeterminate
                 ></v-progress-circular>
             </v-flex>
             <v-flex xs12 sm4 md3 lg3 class="pa-4">
                 <v-img
                     :src="eventDetails.EventImage"
                     :lazy-src="eventDetails.EventImage"
                     width="100%">
                     <v-layout
                         slot="placeholder"
                         fill-height
                         align-center
                         justify-center
                         ma-0
                     >
                         <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
                     </v-layout>
                 </v-img>
             </v-flex>
            <v-flex xs12 sm8 md9 lg9 class="pa-2 py-4 px-3" >
                 <p class="google-font mb-0" style="font-size:150%;color:rgb(2, 119, 189)">{{eventDetails.FeatureEventName}}</p>
                 <span class="google-font mt-1 mb-0 grey--text"  style="font-size:105%">
                     <v-icon small>insert_invitation</v-icon>
                     {{eventDetails.EventDate.Date +'/'+ eventDetails.EventDate.Month +'/'+ eventDetails.EventDate.Year}} 
                     &nbsp;
                     <v-icon small>watch_later</v-icon>
                     {{eventDetails.EventTime.StartTime +' - '+ eventDetails.EventTime.EndTime}}
                     &nbsp;
                     <v-icon small>map</v-icon>
                     {{eventDetails.EventVenue | summery(50)}} <a :href="eventDetails.EventVenueMapLink" target="_blank">(Map)</a>
                 </span>    
                <p class="google-font mt-2 mb-1" style="font-size:115%;color:#757575">
                    {{eventDetails.EventDescription}}
                </p>
                
                 <v-btn color="#1a73e8" v-if="eventDetails.RegistrationLink.length>0" :href="eventDetails.RegistrationLink" target="_blank" rel="noopener" class="ma-0 elevation-0 my-2" dark style="text-transform: capitalize;border-radius:5px;"> 
                     Registration Link
                 </v-btn>
                 &nbsp;

                 <v-tooltip top slot="activator">
                     <v-btn flat :href="eventDetails.EventWebsite" target="_blank" rel="noopener" icon color="#616161" class="ma-0 elevation-0" slot="activator" style="text-transform: capitalize;border-radius:5px;"> 
                         <v-icon>language</v-icon>
                     </v-btn>
                     <span>See {{eventDetails.FeatureEventName}} Website</span>
                 </v-tooltip>

                 <v-tooltip top slot="activator">
                     <v-btn flat  :href="eventDetails.MeetupLink" target="_blank" rel="noopener" icon color="#616161" class="ma-0 elevation-0" slot="activator" style="text-transform: capitalize;border-radius:5px;"> 
                         <v-icon>fab fa-meetup</v-icon>
                     </v-btn>
                     <span>See {{eventDetails.FeatureEventName}} Meetup</span>
                 </v-tooltip>
            
             </v-flex> 
        </v-layout>



        <v-layout wrap align-center justify-center row fill-height class="mt-0 mb-0" >
           <v-flex xs12 md12 lg12 class="pa-2 mb-0">
               <p class="google-font mb-0" style="font-size:170%;color:#0277bd">Upcoming Events</p>
               <p class="google-font mt-0 mb-0" style="font-size:120%">
                   Our events are open to newbies, developers, managers, and organizations who are interested in Google's technologies or use them as part of their projects.
                   To know more about the upcoming meetups visit <a :href="chapterDetails.ChapterUpcomingEventsLink" target="_blank" style="text-decoration:none;color:#0277bd">GDG Kolkata Meetup Group</a>
               </p>     
            </v-flex> 
        </v-layout>

        <v-layout wrap align-center justify-center row fill-height>
            <v-flex xs12 v-if="showLoader">
                <v-progress-circular
                    :size="50"
                    color="blue"
                    indeterminate
                ></v-progress-circular>
            </v-flex>

            <v-flex xs12>
                <v-slide-y-reverse-transition>
                    <v-list two-line subheader v-show="showData" class="grey lighten-5">
                        <v-list-tile
                            v-for="(item,i) in eventsData" :key="i"
                            avatar
                            style="border-color:#e0e0e0;border-width: 1px;border-style: solid;border-top:0; border-left:0; border-right:0; border-bottom:1"
                        >
                            <v-list-tile-avatar>
                                <v-icon>view_compact</v-icon>
                            </v-list-tile-avatar>

                            <v-list-tile-content>
                                <v-list-tile-title class="google-font">{{ item.name }}</v-list-tile-title>
                                <v-list-tile-sub-title class="google-font">{{ item.local_date }} | {{ item.local_time }}</v-list-tile-sub-title>
                            </v-list-tile-content>

                            <v-list-tile-action>
                                <v-btn icon ripple :href="item.link"
                                target="_blank">
                                    <v-icon color="grey lighten-1">arrow_forward</v-icon>
                                </v-btn>
                            </v-list-tile-action>
                            
                        </v-list-tile>
                        

                    </v-list>
                </v-slide-y-reverse-transition>
            </v-flex>
        </v-layout>

    </v-container>
</template>

<script>
import ChapterDetails from '@/assets/data/chapterDetails.json'
import { MeetupAPI } from '@/config/key'
import eventDetails from '@/assets/data/featureEvent.json'


    

export default {
    data() {
        return {
            eventDetails:eventDetails,
            chapterDetails: ChapterDetails,
            eventsData:[],
            showLoader: true,
            showData:false,
            showData1:false
        }
    },
    created(){
        fetch('https://cors.io/?https://api.meetup.com/'+MeetupAPI.urlname+'/events?key='+MeetupAPI.apiKey).then(data=>data.json()).then(res=>{
            
            this.showLoader = false
            this.showData = true
            this.showData1 = true
            this.eventsData = res
        })
    },
    filters:{
        summery: (val,num)=>{
            return val.substring(0,num)+"..."
        },
        dateFilter: (value)=>{
            const date = new Date(value)
            return date.toLocaleString(['en-US'], {month: 'short', day: '2-digit', year: 'numeric'})
        }
    }
}
</script>




