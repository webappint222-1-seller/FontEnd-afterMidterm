<template>
  <div class="bill">
    <Navbar />
    <v-container class="flex">
      <v-layout column>
        <v-flex xs12 sm12 md12 lg12 class="justify-center">
          <v-card flat class="pa-4 mt-10 overflow-y-scroll" dark color="" width="auto" height="600">
            <span class="text-lg white--text">SUMMARY</span>

            <div v-for="cInfo in cartInfo" :key="cInfo.id">
              <v-card dark flat class="w-80 h-auto my-5" color="#C0C0C0">
                <v-layout>
                  <v-card-text class="text-sm white--text">
                    <ul class>
                      <li>
                        <span class>Order Number: {{ cInfo.id }}</span>
                      </li>
                      <li>
                        <span class>Order Name: {{ cInfo.name }} By. {{ cInfo.band }}</span>
                      </li>
                      <li>
                        <span class>Order Price: {{ cInfo.price }} yen</span>
                      </li>                                            
                    </ul>
                  </v-card-text>                                                                
                  <v-card-actions>                    
                    <!-- <v-btn @click="deleteCart(cInfo.id)" color="red darken-4">
                      <v-icon>delete</v-icon>
                    </v-btn> -->
                  </v-card-actions>                  
                </v-layout>
                <div>
                <template>
                          <vue-numeric-input
                            :model-value="1"
                            v-model="quantity"
                            :min="1"
                            :max="10"
                            inline
                            align="center"
                            controls
                            class ="ml-20 mb-5"
                          ></vue-numeric-input>
                        </template>
                        </div>
              </v-card>
            </div>

            <v-card-text class="text-sm truncate white--text">
              <ul justify-center>
                <li class= "mb-4 ml-20">
                  <v-btn
                    v-on:click="countPiece(), countPrice()"
                    :disabled="click"
                    class="mr-12"
                    color="#FFB6C1"
                  >
                    <v-icon>checklist</v-icon>
                  </v-btn>
                </li>

                <li class="mb-2 ml-6 text-xl">
                  <span>Total Quantity: {{ totalQuantity }} Piece</span>
                </li>
                <li class="ml-6 text-xl">
                  <span>Total Price: {{ totalPrice }} yen</span>
                </li>

               
              </ul>          
            </v-card-text>
          </v-card>
        </v-flex>
        <v-flex xs12 sm12 md12 lg12 class="justify-center">
          <v-btn no-gutter dark @click="$router.push('/')" class="mt-10">
            <v-icon left>reply</v-icon>
            <span>BACK TO HOME</span>
          </v-btn>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>

import Navbar from '@/components/Navbar.vue'
import VueNumericInput from 'vue-numeric-input'

export default {
  name: 'Bill',
  data() {
    return {
      cartInfo: [],
      totalQuantity: 0,
      totalPrice: 0,
      url: 'http://localhost:5001/productInfo',
      carturl: 'http://localhost:5002/cartInfo',
      click: false,
      // q: ''
      
    }
  },
  components: {
    Navbar,
    VueNumericInput

  },
  methods: {
    async getCartForm() {
      try {
        const res = await fetch(this.carturl)
        const getcartdata = await res.json()
        return getcartdata

      }
      catch (error) { console.log(`get summary failed: ${error}`) }
    },

    countPiece() {
      console.log(`in loop`)

      for (let i = 0; i < this.cartInfo.length; i++) {
        // let q = this.q
        this.totalQuantity += this.quantity
        this.click = true;
      }

    },

    countPrice() {
      console.log(`in price`)
      for (let i = 0; i < this.cartInfo.length; i++) {
        this.totalPrice += this.cartInfo[i].price *= this.quantity
        this.click = true;
      }
    },

  },

  async created() {
    this.cartInfo = await this.getCartForm()

  }

}
</script>