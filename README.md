<html><head> 
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script> 
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous"> 
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script> 
 </head> 
 <body> 
  <div id="app1" class="container"> 
   <h1>{{titulo}}</h1> 
   <div class="row"> 
    <div class="col"> 
     <ul> 
      <li v-for="poke in pokemones"> <button v-on:click="verPoke(poke.url,poke.name)" class="btn btn-link">{{poke.name}}</button> </li> 
     </ul> 
    </div> 
    <div class="col-sm">
     Imagen del Pokemón 
     <br> 
     <img v-bind:src="urlImagen"> 
     <br> 
     <h3 class="text-danger">{{nombrePoke}}</h3> 
    </div> 
   </div> 
   <div class="row"> 
    <div class="col-sm"> 
     <button v-on:click="pidePokes(siguiente)" class="btn btn-primary"> Siguientes Pokemones</button> Total de Pokemones: {{total}} 
     <button v-on:click="pidePokes(anterior)" class="btn btn-warning"> Pokemones Anteriores</button> 
    </div> 
   </div> 
   <script>
    var app=new Vue({
  el:"#app1",
  data:{  
      titulo: "API de Pokemones",
      urlAPI: "https://pokeapi.co/api/v2/pokemon",
      pokemones : [],  
        totalPokes: 0,
        siguiente: "",
        anterior: "",
        poke:[],
        nombrePoke:"",
        urlImagen:"",
  },  
        mounted(){
        this.pidePokes(this.urlAPI);
            this.verPoke("https://pokeapi.co/api/v2/pokemon/1","colocho")
  },
  methods:
        {
          pidePokes: async function(url) {
              const response = await fetch(url);
            this.pokemones = await response.json();
                this.totalPokes=this.pokemones.count;
                this.siguiente=this.pokemones.next;
                this.anterior=this.pokemones.previous;
                    this.pokemones = this.pokemones.results;
            },
        verPoke: async function(url,nombre){
            const response = await fetch (url);
            this.poke = await response.json();
            this.poke=this.poke.sprites.other
            this.nombrePoke=nombre;
            this.urlImagen=this.poke.dream_world.front_default;
    }
    },        
    }) //fin de objeto Vue
</script> 
  </div>
 
</body></html>
