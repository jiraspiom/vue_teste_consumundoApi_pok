<template>
  <div id="pokemon">
    <div class="card">
      <div class="card-image">
        <figure>
          <img :src="imgCurrent" alt="Placeholder image" />
        </figure>
      </div>
      <div class="card-content">
        <p class="title is-4">{{ pokemon.id }} - {{ name | filtroUpper }}</p>
        <p class="subtitle is-6">{{ pokemon.type }}</p>

        <div class="content"></div>
        <button class="button" @click="mudarSprite">mudar sprite</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  created: function () {
      axios.get(this.url).then((res) => {
      this.pokemon.id = res.data.id;
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.imgCurrent = res.data.sprites.front_default;
      console.log(res.data.types.type.name);
    });
  },
  data() {
    return {
        isFront: true,
        imgCurrent: "",
      pokemon: {
        id: 0,
        type: "",
        front: "",
        back: "",
      },
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  filters: {
    filtroUpper: function (value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },
  methods: {
      mudarSprite: function(){
          if(this.isFront){
              this.isFront = false;
              this.imgCurrent = this.pokemon.back
          }else{
              this.isFront = true;
              this.imgCurrent = this.pokemon.front
          }
      }
  }
};
</script>

<style>
#pokemon {
  margin-top: 2%;
}
</style>