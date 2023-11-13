<template>
            <div class="card">
               <img :src="img" class="card-img-top" :alt="name">
               <div class="card-body text-center ">
                 <h5 class="card-title">{{ name }}</h5>
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
   .card{
    background-color: red;
   }
   </style>