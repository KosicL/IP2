<template>
  <v-app id="inspire">
    <v-app-bar app dark>
      <v-toolbar-title style="display: flex; justify-content: center; align-content: center;">
        <v-img src="https://gamepress.gg/arknights/sites/arknights/files/Arkgnits-main.jpg" contain width="50" style="padding-right: 50px;"></v-img>
        <h3>Arknights Operator List</h3>
      </v-toolbar-title>

      <v-spacer></v-spacer>
      
      <v-btn
        v-for="link in links"
        :key="link.tekst"
        :to="link.path"
        text
      >
        {{ link.tekst }}
      </v-btn>
    </v-app-bar>

  

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>


<script>
  export default {
    data: () => ({
      links:[
        {
          tekst:'Operators',
          path:'/'
        },
        {
          tekst:'Search',
          path:'/search'
        },
      ]
     }),
  }
</script>
