<template>
  <div class="lista_opratora">
    <v-container>
      <v-row>
        <v-col v-for="operator in operators" :key="operator.name">
          <opCard :operator="operator"></opCard>
        </v-col>
      </v-row>
      <template>
        <div class="text-center">
          <v-pagination 
            @input="newPage()"
            v-model="page"
            :length="Math.ceil(this.operatorsAll.length/10)"
            :total-visible="7"
          ></v-pagination>
        </div>
      </template>
    </v-container>
  </div>
</template>

<script>
  import opCard from '@/components/OpCard.vue'

  export default {
    components: {opCard},
    name: 'Home',
    data:()=>({
      page: 1,
      operators: [],
      operatorsAll: [],
    }),

    mounted (){
      this.dohvatiAPI()
    },

    methods:{
      dohvatiAPI: function(){
        this.axios.get('https://rhodesapi.up.railway.app/api/operator').then((response) => {
          this.operatorsAll=response.data
          this.operatorsAll=this.operatorsAll.sort((a, b) => a.name > b.name ? 1 : -1)
          this.newPage()
        })
      },

      newPage: function(){
        this.operators=[]
        let first = (this.page - 1)*10
        let last = this.page*10
        if (last > this.operatorsAll.length){
          last = this.operatorsAll.length
        }
        for (let i = first; i < last; i++){
          this.operators[i - first]=this.operatorsAll[i]
        }
      }
    }
  }
</script>

