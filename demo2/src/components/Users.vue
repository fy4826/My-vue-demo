<template>
  <div class="Users">
    <ul>
      <li @click="user.show=!user.show" v-for="(user,index) in users" :key="index">
        <h2>{{user.name}}</h2>
        <h3 v-show="user.show">{{user.position}}</h3>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
name:'Users',
data(){
    return {
        users:[
            {name:"方研",position:"web前端开发",show:false},
            {name:"电话",position:"15867139271",show:false},
            {name:"邮箱",position:"15867139271@163.com",show:false}
        ]
    }
}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.Users{
    width: 100%;
    max-width: 1900px;
    margin: 40 auto;
    padding: 0 20px;
    box-sizing:border-box;
}
ul{
    display: flex;
    flex-wrap: wrap;
    list-style-type: none;
    padding: 0;

}
li{
    flex-grow: 1;
    flex-basis: 300px;
    text-align: center;
    padding: 30px;
    border: 1px solid #222;
    margin: 10px;
    cursor:pointer;
}
</style>
