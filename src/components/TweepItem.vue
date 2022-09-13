<template>
  <div class="tweep-item" @click="favouriteTweep(tweep.id)">
    <div class="user-profile_tweep">
        <div class="tweep-item_user">
      @{{ username }}
        </div>
        <div class="tweep-item_content">
{{ tweep.content }}
        </div>
    </div>

  </div>
</template>

<script>

export default {
name: 'TweepItem',
props: { 
    username: {
type: String,
required: true
},
tweep:{
    type: Object,
    required: true
}
},
methods:{
    favouriteTweep(id){
        this.$emit('favourite', id)
    }
}
}
</script>

<style>
.tweep-item{
    padding: 20px;
    background-color: white;
    border: 1px solid aquamarine;
    border-radius:5px;
    box-sizing: border-box;
    cursor: pointer;
    transition: all 0.25s ease;
}
.tweep-item_user{
    font-weight:bold;
}
.tweep-item:hover{
    transform: scale(1.1, 1.1); 
}

</style>