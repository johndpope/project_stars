<template>
<v-flex xs12 sm10 offset-sm1>
    <v-container fill-height>
        <v-layout class="justify-center" justify-space-around row wrap text-xs-center>  
            <div v-if="portfolio.length ===0" v-for="(item, index) in portfolio" :key="index">
                <div class="black--text headline">You haven't bought any Items</div>
            </div>
            <div v-if="portfolio.length !=0" v-for="(item, index) in portfolio" :key="index">
                <v-card class="transparent margin_items_portfolio elevation-8">
                        <v-card-title primary-title class="justify-center">
                            <div>
                                <v-avatar v-if="item.img != ''" size="45px"><img :src="item.img" alt=""></v-avatar>
                                <v-avatar v-else-if="item.img === ''&& item.object === 'star'" size="45px">
                                    <img src="https://img.purch.com/w/660/aHR0cDovL3d3dy5zcGFjZS5jb20vaW1hZ2VzL2kvMDAwLzA3My85NTMvb3JpZ2luYWwvc2lyaXVzLmpwZw==" alt="">
                                </v-avatar>
                                <v-avatar v-else-if="item.img === ''&& item.object != 'star'" size="45px">
                                    <img src="http://www.hanedanrpg.com/photos/hanedanrpg/20/96700.jpg" alt="">
                                </v-avatar>
                                <div class="black--text headline">{{item.name}}</div>
                                <div class="black--text subheading">{{item.object}} 
                                    <span v-if="item.object == 'star' && item.name != 'Sun'" class="black--text subheading"> (HD{{item.hd}})
                                        </span></div>
                                <div class="black--text subheading">Price: {{item.price}}
                                    <v-icon color="black" small>fab fa-ethereum</v-icon>
                                </div>
                            </div>
                        </v-card-title>
                        <v-expansion-panel dark>
                            <v-expansion-panel-content>
                                <div slot="header">Actions</div>
                                <v-divider></v-divider>
                                    <v-card-text>
                                        <v-layout class="justify-center"> 
                                        </v-layout>
                                        <v-layout class="justify-center" row wrap align-center> 
                                            <v-flex xs8>
                                                <v-text-field
                                                    prepend-icon="fab fa-ethereum"
                                                    color="green darken-2"
                                                    label="Selling Price in ETH"
                                                    :value="item.price"
                                                    :rules="[]"
                                                    dark
                                                ></v-text-field>
                                            </v-flex>
                                            <v-btn outline color="green darken-2">Change</v-btn>
                                        </v-layout>
                                        <v-layout v-if="item.object == 'star'" class="justify-center" row wrap align-center>
                                            <v-flex xs8>
                                                <v-text-field
                                                    prepend-icon="fas fa-exchange-alt"
                                                    color="green darken-2"
                                                    label="Name"
                                                    :value="item.name"
                                                    :rules="[]"
                                                    dark
                                                ></v-text-field>
                                            </v-flex>
                                            <v-btn outline color="green darken-2">Change</v-btn>
                                        </v-layout>
                                    </v-card-text>
                            </v-expansion-panel-content>
                        </v-expansion-panel>
                 </v-card>
            </div>
        </v-layout>
    </v-container>
</v-flex>
</template>

<script>
import api from "@/api";
export default {
  name: 'Portfolio',
  data() {
    return {
        portfolio:[]
    }
  },
  created() {
      this.getPortfolio();
  },
  methods: {
      getPortfolio() {
        api.getPortfolio(portfolio => {
          this.portfolio = portfolio;
        })
      }
  }
}
</script>
<style>
    .margin_items_portfolio {
        width: 350px;
        margin-bottom: 2vh;
    }
</style>
