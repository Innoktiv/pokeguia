 <template>
    <div>
        <img src="../assets/pokemon-logo.png" alt="">
        <h1> Pokeguia </h1>
        <form>
          <label for="hola">Nombre</label>
          <!-- v-model creates a 2 way binding on  a form input element -->
          <input type="text" v-model="personaje.name">         
          <!-- v-on -->
          <input type="submit" @click.prevent="fetchCharacter" value="Buscar">
        </form>
        <section>
          <img :src="image" alt="img ">
          <h2>Movimientos</h2>
          <div>
            <ul>
              <li v-for="movimiento in movimientos" :key="movimiento.move"> {{ movimiento.move.name}}</li>
            </ul>
          </div>
          <h2>Habilidad</h2>
          <div>
            <ul>
              <li v-for="habilidad in habilidades" :key="habilidad.ability"> {{habilidad.ability.name}}

              </li>
            </ul>
          </div>
        </section>
    </div>
    
</template>

<script>
export default {
    name: 'pokemon',
    // props: {},
    data: function(){
        return {
            personaje:{
              name:'pikachu',
              id: '', 
              sprites:'', 
              moves:'',
              ability: ''
            }
        }
    },
    computed: {
      image(){
        return this.personaje.sprites.front_default
      }, 
      movimientos(){
        return this.personaje.moves
      },
      habilidades(){
        return this.personaje.abilities
      }
    },
    methods: {
      // PETICION A LA API (Conexion)
        fetchCharacter(){
          fetch(`https://pokeapi.co/api/v2/pokemon/${this.personaje.name}`)
          // COMO ES PROMESA QUE RETORNA UN JSON
            .then(response=> response.json())
            
            .then(json=>{
              // REGRESAR LO QUE VIENE DE RESPUESTA
              console.log(json)
         this.addCharacter(json)
            })
            .catch(error=>{
              console.log(error);
            })
        },

        addCharacter(pokemon){
          this.personaje = pokemon;
          console.log(pokemon)
          // if(json.results[0]=== undefined){
          //   alert("No encontrado")
          //   return;
          // }else{
          //   this.personaje = json.results
          // }
        }
    },
    
    // -- Lifecycle Methods

    // beforeCreate(){
    //     console.log("beforeCreate");
    //     console.log(this.text);
    // },
    created(){
        this.fetchCharacter(); 
    },
    // beforeMount(){
    //     console.log("beforeMounted");
    // },
    // mounted(){
    //     console.log("mounted");

    // },
    // beforeUpdate(){
    //     console.log("beforeUpdate");
    // },
    // updated(){
    //     console.log("updated");
    // },
    // beforeDestroy(){
    //     console.log("beforeDestroy");
    //     console.log(this.text);
    // },
    // destroyed(){
    //     console.log("destroyed");
    //     console.log(this.text);
    // }
    // -- End Lifecycle Methods
}
</script>

<style scoped>
    
</style>