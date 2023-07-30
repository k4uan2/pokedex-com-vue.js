<template>
  <div id="main-pokemon"> 
      <div class="card">
      <div class="card-image">
        <figure>
        <img :src="currentImage" alt="Placeholder image">
      </figure>
      </div>
      <div class="card-content">
      <div class="media">
        
        <div class="media-content">
          <p class="title is-4">{{upperName(name)}}</p>
          <p class="subtitle is-6">{{pokemon.type}}</p>
        </div>
      </div>

      <div class="content">
        <button class="button is-small" @click="changeSprite">Mudar sprite</button>
      </div>
      </div>
     </div>

  </div>
</template>

<script>
import axios from "axios"
export default {
  name: 'Pokemon',
  created: function(){
    axios.get(this.url).then(res => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.currentImage = this.pokemon.front
    })
  },  
  data(){
    return{
      isFront: true,
      currentImage: '',
      pokemon: {
        type: '',
        front: '',
        back: ''
      }
    }
  },
  props: {
    name: String,
    url: String,
    num: Number
  }, 
  methods: {
    upperName: function(value){
      let newName = value[0].toUpperCase() + value.slice(1)
      return newName
    },
    changeSprite: function(){
      if(this.isFront){
        this.isFront = false
        this.currentImage = this.pokemon.back
      }else{
        this.isFront = true
        this.currentImage = this.pokemon.front
      }
    }
  }
}
</script>

<style>
  #main-pokemon{
    margin-top: 2%;
  }
</style>