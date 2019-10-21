<template>
<footer>
    <p>{{copyright}}</p>
</footer>
</template>

<script>
export default {
name:'Footer',
data(){
    return {
        copyright:'Copyright 2019 Vue.js Demo2'
    }
}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
footer{
    background-color:#222;
    padding: 10px;
}
p{
    text-align: center;
    color:#fff;
}
</style>
