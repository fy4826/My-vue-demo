<template>
<header>
    <h1>{{title}}</h1>
</header>
</template>

<script>
export default {
name:'Header',
data(){
    return {
        title:'Vue.js Demo2'
    }
}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
header{
    background-color:skyblue;
    padding: 20px;
}
h1{
    text-align: center;
    color: black;
}
</style>
