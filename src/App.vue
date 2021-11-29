<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      Score board Flechete maison
    </v-app-bar>

    <v-main>
        <v-slider
          class="sliderNbr"
          v-model="nbrUser"
          color="orange"
          label="Nombre joueurs"
          hint="Mahaiza mapisa nory"
          min=1
          max=10
          thumb-label
        ></v-slider>
      <v-row>
        <v-card
          class="mx-auto"
          max-width="344"
          v-for="(joueur, n) in joueurs" 
          :key="n"
        >
          <v-card-title>{{joueur.name}} : {{joueur.score}}</v-card-title>
          <v-col
            cols="12"
            md="12"
          >
            <v-text-field
              v-model="joueur.name"
              color="purple darken-2"
              label="Joueur ID"
            ></v-text-field>
            <v-text-field
              color="purple darken-2"
              label="Score"
              v-model="joueur.additionalScore"
            >
              <v-icon
                slot="append"
                color="red"
                @click="add_score(n)"
              >
                mdi-plus
              </v-icon>
              <v-icon
                slot="prepend"
                color="green"
                @click="remove_score(n)"
              >
                mdi-minus
              </v-icon>
            </v-text-field>
          </v-col>
        </v-card>
      </v-row>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  components: {
  },
  data () {
    return {
      nbrUser : 1,
      listJoueur : [],
      joueurs : []
    }
  },

  watch:{
    "nbrUser" : async function(newValue){
        this.listJoueur=[]
        for(let i=0; i<newValue; i++){
          this.listJoueur[i] = {
            name:'NAME',
            score: 0,
            additionalScore: 0
          }
        }
    },
    "listJoueur" : {
      deep: true,
      handler(val){
        this.joueurs = [...val]
      }
    }
  },

  methods: {
      add_score(key) {
          let to_add=parseInt(this.listJoueur[key].additionalScore)
          this.listJoueur[key].score += to_add
          this.listJoueur[key].additionalScore = ''
      },
      remove_score(key) {
          let to_remove=this.listJoueur[key].additionalScore
          this.listJoueur[key].score -= to_remove
          this.listJoueur[key].additionalScore = ''
      },

  }


};
</script>

<style scoped>
.sliderNbr{
  margin-top: 40px;
}
</style>
