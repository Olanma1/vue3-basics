<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
        <h1 class="user-profile_username">@{{ user.username }}</h1>
        <div class="user-profile_admin-badge" v-if="user.isAdmin">Admin</div>
        <div class="user-profile_follower-count">
            <strong>Followers: </strong> {{ followers }}
        </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'UserProfile',
  data(){
    return{
      followers: 0,
      user: {
        id: 1,
        username: 'olanma',
        firstName: 'Mary',
        lastName: 'Olanma',
        email: 'olanmamary2@gmail.com',
        isAdmin: true,
      }
    }
    
  },

  watch: {
 followers(newfollowerCount, oldfollowerCount){
  if(oldfollowerCount < newfollowerCount){
    console.log(`${this.user.username} has a new follower!`)
  }
 }
  },
  computed: {
fullName(){
  return this.user.firstName + '' + this.user.lastName;
}
},
methods: {
  followUser(){
this.followers++
  }
},
mounted() {
  this.followUser();
}
  }

</script>

<style>
.user-profile{
    display: grid;
    grid-template-columns: 1fr 3fr;
    width:100%;
    padding:54px 5%
}
.user-profile_user-panel{
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid blue;
}
h1{
    margin: 0;
}
.user-profile_admin-badge{
    background: rebeccapurple;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 20px;
    font-weight: bold;
}
</style>