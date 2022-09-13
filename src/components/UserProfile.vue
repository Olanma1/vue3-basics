<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
        <h1 class="user-profile_username">@{{ user.username }}</h1>
        <div class="user-profile_admin-badge" v-if="user.isAdmin">Admin</div>
        <div class="user-profile_follower-count">
            <strong>Followers: </strong> {{ followers }}
        </div>
<form class="user-profile_create-tweep" @submit.prevent="addNewTweep">
  <label for="newTweep"><strong>New Tweep</strong></label>
  <textarea id="newTweep" rows="4" v-model="newTweep" />
<button>Tweep</button>
</form>

    </div>
    <div class="user-profile_tweeps-wrapper">
      <TweepItem 
        v-for="tweep in user.tweeps" 
        :key="tweep.id" 
        :username="user.username" 
        :tweep="tweep" 
        @favourite="toggleFavourite"
      />
    </div>
  </div>
</template>

<script>
import TweepItem from './TweepItem.vue';
export default {
    name: "UserProfile",
    data() {
        return {
          newTweep: '',
            followers: 0,
            user: {
                id: 1,
                username: "olanma",
                firstName: "Mary",
                lastName: "Olanma",
                email: "olanmamary2@gmail.com",
                isAdmin: true,
                tweeps: [
                    { id: 1, content: "Social media is fun" },
                    { id: 2, content: "My second post" }
                ]
            }
        };
    },
    watch: {
        followers(newfollowerCount, oldfollowerCount) {
            if (oldfollowerCount < newfollowerCount) {
                console.log(`${this.user.username} has a new follower!`);
            }
        }
    },
    computed: {
        fullName() {
            return this.user.firstName + "" + this.user.lastName;
        }
    },
    methods: {
        followUser() {
            this.followers++;
        },
        toggleFavourite(id){
          console.log(`Favourited tweep #${id}`)
        },
  addNewTweep(){
    if(this.newTweep !== 'draft'){
    this.user.tweeps.unshift({
    id: this.user.tweeps.length + 1,
    content: this.newTweep
  })
}
   this.newTweep = ''
        }
    },
    mounted() {
        this.followUser();
    },
    components: { TweepItem }
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
.user-profile_tweeps-wrapper{
  display: grid;
  grid-gap: 10px;
}
.user-profile_create-tweep{  
  padding-top: 20px;
  display: flex;
  flex-direction: column;
}
</style>