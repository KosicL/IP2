<template>
    <v-card
    class="mx-auto my-12"
    width="315"
    height="475"
    max-width="374"
    dark
    style="padding: 30px;">
        <v-img :src="operator.art[0].link" :lazy-src="operator.art[0].link" eager style="height: 250px; width: fit-content;"></v-img>
        <v-card-title class="card_title" style="padding-bottom: 5px; justify-content: center;"><h5>{{ operator.name }}</h5></v-card-title>
        <v-card-title style="padding: 0px; padding-bottom: 5px; justify-content: center;">
        <div v-for="n in operator.rarity" :key="n"><v-img src="https://gamepress.gg/sites/arknights/files/2019-10/star.png"></v-img></div></v-card-title>
        <v-divider></v-divider>
        <v-card-text style="padding-left: 0px; padding-right: 10px;">
            <div style="display: flex; padding-bottom: 5px; align-items: center; justify-content: center;"><img :src="class_pic(operator.class[0])" style="height: 22px; padding-right: 5px;"><h3>{{ operator.class[0] }}</h3></div>
        </v-card-text>
        <v-card-actions style="justify-content: center;">
            <v-btn :href="operator.url" block text color="red" absolute bottom>More Information</v-btn>
        </v-card-actions>
    </v-card>
</template>

<script>
    export default{
        name:'opCard',
        props:['operator'],

        methods: {
            class_pic(n){
                if(n=='Vanguard'){
                    return "https://gamepress.gg/arknights/sites/arknights/files/styles/50x50/public/2019-06/icon_profession_pioneer_large.png?itok=03pbuMXs"
                }
                else if(n=='Guard'){
                    return "https://gamepress.gg/arknights/sites/arknights/files/styles/50x50/public/2019-06/icon_profession_warrior_large.png?itok=4_Z3qY4r"
                }
                else if(n=='Defender'){
                    return "https://gamepress.gg/arknights/sites/arknights/files/styles/50x50/public/2019-06/icon_profession_tank_large.png?itok=zUT17t1v"
                }
                else if(n=='Sniper'){
                    return "https://gamepress.gg/arknights/sites/arknights/files/styles/50x50/public/2019-06/icon_profession_sniper_large.png?itok=z1-BlwaY"
                }
                else if(n=='Caster'){
                    return "https://gamepress.gg/arknights/sites/arknights/files/styles/50x50/public/2019-06/icon_profession_caster_large.png?itok=WPXbCQEc"   
                }
                else if(n=='Medic'){
                    return "https://gamepress.gg/arknights/sites/arknights/files/styles/50x50/public/2019-06/icon_profession_medic_large.png?itok=akdh0URg"
                }
                else if(n=='Supporter'){
                    return "https://gamepress.gg/arknights/sites/arknights/files/styles/50x50/public/2019-06/icon_profession_support_large.png?itok=4CDPHCst"   
                }
                else{
                    return "https://gamepress.gg/arknights/sites/arknights/files/styles/50x50/public/2019-06/icon_profession_special_large.png?itok=xfxLuEOO"
                }
            },
        }
    }
</script>
