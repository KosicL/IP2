<template>
  <div class="lista_opratora">
    <v-container>
      <div style="display: flex; height: 30px; justify-content: center; align-content: center; padding-top: 20px; padding-bottom: 50px;">
        <v-expansion-panels style="width: 150px;">
          <v-expansion-panel>
            <v-expansion-panel-header>
              Search by
            </v-expansion-panel-header>
            <v-expansion-panel-content>
              <v-btn block text @click="searchName()">Name</v-btn>
            </v-expansion-panel-content>
            <v-expansion-panel-content>
              <v-btn block text @click="searchClass()">Class</v-btn>
            </v-expansion-panel-content>
            <v-expansion-panel-content>
              <v-btn block text @click="searchRarity()">Rarity</v-btn>
            </v-expansion-panel-content>
          </v-expansion-panel>
        </v-expansion-panels>
        <v-autocomplete color=black large :label="labelText" v-model="search" :items="items" @change="newSearch()" style="padding-left: 10px;"></v-autocomplete>
      </div>
      <v-row v-if="showName">
        <v-col>
          <opCard :operator="operators"></opCard>
        </v-col>
      </v-row>
      <v-row v-if="show">
        <v-col v-for="operator in operatorsShown" :key="operator.name">
            <opCard :operator="operator"></opCard>
        </v-col>
      </v-row>
    <template v-if="show">
        <div class="text-center">
          <v-pagination 
            @input="newPage()"
            v-model="page"
            :length="Math.ceil(this.operators.length/10)"
            :total-visible="7"
          ></v-pagination>
        </div>
      </template>
    </v-container>
    <v-overlay :value="overlay" @click="overlay=!overlay">
      <v-alert dense type="error" dark max-width="500">Operator not found</v-alert>
    </v-overlay>
  </div>
</template>
  

<script>
  import opCard from '@/components/OpCard.vue'
  
  export default {
    components: {opCard},
    name: 'Home',
    data:()=>({
      operators: [],
      operatorsShown: [],
      operatorsAll: [],
      page: 1,
      type: 'operator/',
      show: false,
      showName: false,
      overlay: false,
      labelText: 'Search by Name',
      search: '',
      items: [],
      names: [],
      classes: ['Vanguard', 'Guard', 'Defender', 'Sniper', 'Caster', 'Medic', 'Supporter', 'Specialist'],
      rarity: ['6', '5', '4', '3', '2', '1']
    }),

    mounted (){
      this.dohvatiImena()
    },
  
    methods:{
      newSearch: function(){
        if(this.search==null){
          this.show=true
          this.showName=false
          this.operators=this.operatorsAll
          this.page=1
          this.newPage()
        }
        else if (this.labelText=='Search by Name'){
          this.show=false
          this.showName=true
          this.dohvatiAPI()
        }
        else{
          this.show=true
          this.showName=false
          this.dohvatiAPI()
        }
      },

      searchName: function(){
        this.type='operator/'
        this.labelText='Search by Name'
        this.items=this.names
      },
      searchClass: function(){
        this.type='search?class='
        this.labelText='Search by Class'
        this.items=this.classes
      },
      searchRarity: function(){
        this.type='search?rarity='
        this.labelText='Search by Rarity'
        this.items=this.rarity
      },
      dohvatiImena: function(){
        this.axios.get('https://rhodesapi.up.railway.app/api/operator').then((response) => {
          this.operatorsAll=response.data
          this.operatorsAll=this.operatorsAll.sort((a, b) => a.name > b.name ? 1 : -1)
          for (let i=0; i<this.operatorsAll.length; i++){
            this.names[i]=this.operatorsAll[i].name
          }
          this.items=this.names
        })
      },

      dohvatiAPI: function(){
        this.axios.get('https://rhodesapi.up.railway.app/api/'+ this.type + this.search)
          .then((response) => {
            console.log(response.data)
            this.operators=response.data
            this.page=1
            this.newPage()
          })
          .catch((error) => {
            console.log(error.response.status)
            this.overlay=true
        })
      },

      newPage: function(){
        this.operatorsShown=[]
        let first = (this.page - 1)*10
        let last = this.page*10
        if (last > this.operators.length){
          last = this.operators.length
        }
        for (let i = first; i < last; i++){
          this.operatorsShown[i - first]=this.operators[i]
        }
      }
    }
  }
</script>
