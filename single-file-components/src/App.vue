<template>
   <div id="app">
       <div class="inner">
           <div class="ratingContainer">
               <span class="bigRating" v-html="bigRating"></span>
               <div class="rating-stars">
                   <star
                       v-for="index in 5"
                       v-bind:key="index"
                       v-bind:weight="index"
                       v-bind:enabled="enabled"
                       v-bind:currentrating="currentRating"
                   ></star>
               </div>
           </div>
           <sum v-bind:ratings="ratings"></sum>
       </div>
   </div>
</template>

<script>
import star from './components/Star'
import sum from './components/Summary'

export default {
 name: 'App',
 components: {star, sum},
 data: function() {
       return {
           currentRating: 0,
           bigRating: '0',
           enabled: true,
           ratings: [
               {
                   weight: 1,
                   votes: 0
               },
               {
                   weight: 2,
                   votes: 0
               },
               {
                   weight: 3,
                   votes: 0
               },
               {
                   weight: 4,
                   votes: 0
               },
               {
                   weight: 5,
                   votes: 0
               }
           ]
       }
 },
 methods: {
 },
 created: function() {
     if(localStorage.ratings)
     {
         this.ratings = JSON.parse(localStorage.ratings);
     }
 }
}
</script>

<style>
@import url(https://fonts.googleapis.com/css?family=Roboto:100,300,400);
@import url(https://netdna.bootstrapcdn.com/font-awesome/3.2.1/css/font-awesome.css);
#app {
   width: 400px;
}
.ratingContainer {
   float: left;
   width: 45%;
   margin-right: 5%;
   text-align: center;
}
.summaryContainer {
   float: left;
   width: 50%;
   font-size: 13px;
}
.bigRating {
   color: #333333;
   font-size: 72px;
   font-weight: 100;
   line-height: 1em;
   padding-left: 0.1em;
}
.rating-stars .hover {
   color:yellow;
}
.rating-stars {
   font-size: 20px;
   color: #E3E3E3;
   margin-bottom: .5em;
}
.rating-stars .active {
   color: #737373;
}
</style>