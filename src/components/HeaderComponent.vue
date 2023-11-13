<template>
    <header class="p-3">
         <h1 class="container">{{ title }}</h1>
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
</style>