<template>
    <v-container class="pa-0" style="max-width:100vw!important;">
        <v-layout wrap align-center justify-center row fill-height>
           <v-img xs12 sm12 md12 lg12 xl12
                    :src="require('@/assets/img/banner.jpg')"
                    :lazy-src="require('@/assets/img/banner.jpg')"
                    gradient="rgba(0,0,0,.65), rgba(0,0,0,.65)"
                    width="100%" max-height="90vh" style="padding:20px">
                     <v-layout wrap align-center justify-center row fill-height style="color:#fff">
                   <v-flex xs12 sm7 md8 lg8 xl8 class="">
                <p class="google-font mb-1" style="font-weight: 350;color: #fff;font-size:300%;line-height:1"><b>Make good things 
                    <span style="color: #1a73e8;">together</span>.</b>
                </p>
                <p class="google-font mt-0" style="font-size:180%;">{{chapterDetails.ChapterName}}</p>
                <p class="google-font" style="font-size:110%">{{chapterDetails.ChapterShortDescription}}</p>
                <p class="google-font" style="font-size:110%;color:#fff">
                    <span v-for="(item,i) in chapterDetails.ChapterHashTags" :key="i">
                        #{{item}} &nbsp;
                    </span>
                </p>

                <v-btn :href="chapterDetails.ChapterMeetupLink" target="_blank" class="ma-0 google-font elevation-1" color="#1a73e8" style="text-transform: capitalize;border-radius:5px;color:white">Become a Member</v-btn>

                &nbsp;

                <v-btn :href="chapterDetails.GDGProgramWebsite" target="_blank" round color="cyan" style="text-transform: capitalize;border-radius:5px;text-transform: capitalize;" outline  class="ml-0" dark>Learn More</v-btn>

            </v-flex>
</v-layout>
            </v-img>
            
        </v-layout>

    </v-container>
</template>

<script>
import ChapterDetails from '@/assets/data/chapterDetails.json'
export default {
    data() {
        return {
            chapterDetails: ChapterDetails
        }
    },
}
</script>
