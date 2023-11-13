<template>
            <div class="card border-0 rounded-0 ">
               <img :src="img" class="card-img-top" :alt="name">
               <div class="card-body text-center ">
                 <h5 class="card-title text-light text-uppercase fw-bolder ">{{ name }}</h5>
                 <h5 class="card-title">{{ species }}</h5>
               </div>
             </div>
   </template>
   
   <script>
   
       export default {
         name:'CardsComponent',
         props:{
           img:String,
           name:String,
           species:String,
         },
           data(){
               return{
                
               }
           },
          
       }
   </script>
   
   <style lang="scss" scoped>
   @use '../assets/styles/partials/variables' as *;
   .card{
    background-color: $bgYellow;
   }
   </style>