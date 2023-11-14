<template>
    <header class="p-3 d-flex align-items-center ">
        <img src="/public/image/Yugioh_anime_logo.webp" alt="logo" class="logo">
         <h1 >{{ title }}</h1>
    </header>
</template>

<script>
    export default {
        name:'HeaderComponent',
        data(){
            return{
                title:'Yu-Gi-oh Api'
            }
        }
    }
</script>

<style lang="scss" scoped>
header{
    background-color: white;
}
.logo{
    width:5%;
    height: 25px;
}
</style>