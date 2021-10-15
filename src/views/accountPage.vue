<template>
  <div class="account">
    <Navbar />
    <v-container class="flex">
       <v-flex xs12 sm12 md12 lg12 class="justify-center">
       <!-- <v-btn dark v-show="!addedit" v-on:click="toggleDone()" class="mt-10">
          <span>add / edit</span>
        </v-btn>

        <div v-show="addedit" class="justify-center">
          <v-btn dark v-on:click="toggleDone()" class="mt-10 ml-28">
            <span>cancel</span>
          </v-btn>
          <v-card dark class="w-80 h-auto mt-10">
            <v-card-text>
              <validation-observer ref="observer" v-slot="{ invalid }">
                <form>
                  <validation-provider v-slot="{ errors }" name="Product Name" rules="required">
                    <v-text-field
                      v-model="nameForm"
                      :error-messages="errors"
                      label="Product Name"
                      required
                      single-line
                    ></v-text-field>
                  </validation-provider>

                  <validation-provider v-slot="{ errors }" name="Band Name" rules="required">
                    <v-text-field
                      v-model="bandForm"
                      :error-messages="errors"
                      label="Band Name"
                      required
                      single-line
                    ></v-text-field>
                  </validation-provider>

                  <validation-provider v-slot="{ errors }" name="Price" rules="required|numeric">
                    <v-text-field
                      v-model.number="priceForm"
                      :error-messages="errors"
                      label="Price"
                      required
                      single-line
                      type="number"
                    ></v-text-field>
                  </validation-provider>

                  <validation-provider
                    v-slot="{ errors }"
                    name="Product Description"
                    rules="required|max:1000"
                  >
                    <v-textarea
                      v-model="desForm"
                      :error-messages="errors"
                      :counter="1000"
                      label="Producr Description"
                      required
                      single-line
                    ></v-textarea>
                  </validation-provider>

                  <validation-provider v-slot="{ errors }" name="Product Image" rules="required">
                    <v-file-input
                      :error-messages="errors"
                      label="Image Input"
                      filled
                      required
                      single-line
                      prepend-icon="mdi-camera"
                      type="file"
                      @change="uploadImage"
                      v-model="fileForm"
                    ></v-file-input>
                    <img
                      :src="i"
                      class="h-20 w-40 object-cover border-2 border-black rounded my-4 hidden"
                    />
                  </validation-provider>
                  @change="uploadImage"
                  <v-btn
                    class="mr-4"
                    @click.prevent="submitProductForm"
                    type="submit"
                    :disabled="invalid"
                  >Submit</v-btn>
                  <v-btn @click="clear">Clear</v-btn>
                </form>
              </validation-observer>
            </v-card-text>
          </v-card> 
        </div> -->
      </v-flex>
    </v-container>
    <!-- ----------------------------------------------------------------------------------------------------------- -->
    <!-- Dummy -->
    <v-container class="flex mb-40">
      <v-layout row wrap>
        <v-flex xs12 sm6 md6 lg2 wrap v-for="a in infoAccounts" :key="a.id" class="justify-center">
          <v-card dark flat class="pa-2 w-44 h-auto my-10">
            <!-- <v-responsive>
              <img :src="p.pic" class="w-40 h-40" />
            </v-responsive> -->
            <v-card-text class="justify-center text-xs break-words white--text">
              <ul>
                <li>username: </li>
                <li>{{ a.username }}</li>
                <li class="pt-2">password: </li>
                <li>{{ a.password }}</li>
                <li class="pt-2">firstname: </li>
                <li>{{ a.firstname }}</li>
                <li class="pt-2">lastname: </li>
                <li>{{ a.lastname }}</li>
                <li class="pt-2">nickname: </li>
                <li>{{ a.nickname }}</li>
                <li class="pt-2">tel: </li>
                <li>{{ a.tel }}</li>
              </ul>
            </v-card-text>
           
            <v-card-actions>
              <v-btn @click="deleteAccount(a.id)" class= "" color="red darken-4" small>
                <v-icon small>delete</v-icon>
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>

    <!---------------------------------------------------------------------------------------------------------------->

    <!-- <v-container class="flex mb-40">
      <v-layout row wrap>
        <v-flex xs12 sm6 md6 lg3 wrap v-for="uta in productInfo" :key="uta.id" justify-center>
          <v-card dark flat class="pa-2 w-44 h-auto my-10">
            <v-responsive>
              <img :src="uta.file" class="w-40 h-40" />
            </v-responsive>
            <v-card-text class="justify-center text-xs break-words white--text">
              <ul>
                <li>{{ uta.name }}</li>
                <li class="pt-2">{{ uta.band }}</li>
                <li class="pt-2">{{ uta.price }} yen</li>
                <li class="pt-2">{{ uta.des }}</li>
              </ul>
            </v-card-text>

            <v-card-actions class="justify-center">
              

              <v-btn
                @click.prevent="productInCart(uta)"
                
                color="#FFB6C1"
                small
              >
               
                <v-icon small>shopping_cart</v-icon>
              </v-btn>
            </v-card-actions>

            <v-card-actions class="justify-center">
              <v-btn @click="showProduct(uta)" color="yellow darken-4" small>
                <v-icon small>edit</v-icon>
              </v-btn>
              <v-btn @click="deleteProduct(uta.id)" color="red darken-4" small>
                <v-icon small>delete</v-icon>
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-flex>
      </v-layout>

      <v-layout column wrap mt-8>
        <v-flex xs12 sm12 md12 lg12 wrap class="justify-center hidden-xs-only">
          <v-card flat class="pa-4 overflow-y-scroll" color="black" width="300" height="520">
            <span class="text-lg white--text">CART</span>

            <div v-for="cInfo in cartInfo" :key="cInfo.id">
              <v-card dark flat class="w-auto h-auto my-5" color="#C0C0C0">
                <v-layout wrap>
                  <v-card-text class="justify-start text-sm w-40 truncate white--text">
                    <span>{{ cInfo.name }}</span>
                  </v-card-text>
                  <v-card-actions>
                    <v-btn @click="deleteCart(cInfo.id)" color="red darken-4">
                      <v-icon>delete</v-icon>
                    </v-btn>
                  </v-card-actions>
                </v-layout>
              </v-card>
            </div>

            <v-layout class="justify-center mt-4">
              <v-tooltip bottom>
                <template v-slot:activator="{ on, attrs }">
                  <v-btn
                    @click="$router.push('/billpage')"
                    v-bind="attrs"
                    v-on="on"
                    color="#FFB6C1"
                    dark
                  >
                    <v-icon>shopping_basket</v-icon>
                  </v-btn>
                </template>
                <span>Check Out</span>
              </v-tooltip>
            </v-layout>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container> -->
    <Footer></Footer>
  </div>
</template>

<script>

import Navbar from '@/components/Navbar.vue'
import Footer from '@/components/Footer.vue'
// import { required, max, max_value, numeric } from 'vee-validate/dist/rules'
// import { extend, ValidationObserver, ValidationProvider, setInteractionMode } from 'vee-validate'
// import VueNumericInput from 'vue-numeric-input'

// setInteractionMode('eager')

// extend('required', {
//   ...required,
//   message: '{_field_} can not be empty',
// })

// extend('max', {
//   ...max,
//   message: '{_field_} may not be greater than {length} characters',
// })

// extend('max_value', {
//   ...max_value,
//   message: '{_field_} may not be greater than 10 piece',
// })

// extend('numeric', {
//   ...numeric,
//   message: '{_field_} must be number',
// })

export default {
  name: 'acPage',
//   props: [''],
  data() {
    return {
    //   products: [
    //     { title: "Sakaseya Sakase [Regular Edition]", band: "EGOIST", price: "1204yen", des: "Much anticipated new release featured as main theme to hit anime's theatrical release.", pic: "VVCL-1443.jpg", id: 1 },
    //     { title: "Greatest Hits 2011-2017 Alter Ego [Regular Edition]", band: "EGOIST", price: "2778yen", des: "First greatest hits album of EGOIST featuring 15 titles (13 from anime series) in remastered edition.", pic: "VVCL-1155.jpg", id: 2 },
    //     { title: "Kabaneri of the Iron Fortress [Regular Edition]", band: "EGOIST", price: "1204yen", des: "EGOIST brings the seventh single. The title song is an intro theme for the TV anime series Kabaneri of the Iron Fortress.", pic: "SRCL-9070.jpg", id: 3 },
    //     { title: "RELOADED [Regular Edition]", band: "EGOIST", price: "1300yen", des: "New single release from Egoist is used as main theme for Project Itoh anime.", pic: "SRCL-8927.jpg", id: 4 },
    //   ],
      addedit: false,
      cancel: false,
      nameForm: '',
      bandForm: '',
      priceForm: '',
      desForm: '',
      quanForm: '',
      defaultQuantity: 1,

      fileForm: null,
      addCart: '',
      cartInfo: [],
      productInfo: [],
      infoAccounts:[],
      inEditMode: false,
      addCartMode: false,
      editId: '',
      addCartId: '',
      disabledbtn: false,
      cart: '',

      i: 'https://files.catbox.moe/vq3v5e.png',
      url: 'http://localhost:5001/productInfo',
      carturl: 'http://localhost:5002/cartInfo',
      accounturl: 'http://localhost:5000/infoAccounts',
      // url: 'https://www.utastore.team:3006'

    }

  },

  components: {
    Navbar,
    Footer,
    // ValidationProvider,
    // ValidationObserver,
    // VueNumericInput,

  },

  computed: {

  },

  methods: {
    // disabled() {
    //   this.productInfo.name === this.cartInfo.name
    //   this.disabledbtn = true;
    // },

    // toggleDone() {
    //   this.addedit = !this.addedit
    // },

    clear() {
      this.$refs.observer.reset()
      this.name = ''
      this.band = ''
      this.price = ''
      this.des = ''

    },

    // uploadImage(p) {
    //   const varFile = p.target.files[0]
    //   //console.log(this.fileForm)
    //   if (varFile.type.includes('image')) {
    //     const readImage = new FileReader()
    //     readImage.onload = (e) => {
    //       this.i = e.target.result
    //     }
    //     this.fileForm = varFile
    //     readImage.readAsDataURL(varFile)
    //   }
    // },

    submitProductForm() {
      this.$refs.observer.validate()
      this.nameErrors = this.nameForm === ''
      this.bandErrors = this.bandForm === ''
      this.priceErrors = this.priceForm === ''
      this.desErrors = this.desForm === ''
      this.fileErrors = this.fileForm === null


      console.log(`productName: ${this.nameForm}`)
      console.log(`bandName: ${this.bandForm}`)
      console.log(`productPrice: ${typeof this.priceForm}`)
      console.log(`productDes: ${this.desForm}`)
      console.log(`image: ${this.fileForm}`)

      if (this.Formname !== '' &&
        this.bandForm !== '' &&
        this.priceForm !== '' &&
        this.desForm !== '' &&
        this.fileForm !== null) {
        // this.productInfo.push({
        //   name: this.nameForm,
        //   band: this.bandForm,
        //   price: this.priceForm,
        //   des: this.desForm

        // })
        // EDIT-2
        if (this.inEditMode) {
          this.editProduct({
            id: this.editId,
            name: this.nameForm,
            band: this.bandForm,
            price: this.priceForm,
            des: this.desForm
          })
        }
        else {
          this.addNewProductForm({
            name: this.nameForm,
            band: this.bandForm,
            price: this.priceForm,
            des: this.desForm,
            file: this.fileForm
          })
        }

      }
      this.nameForm = '',
        this.bandForm = '',
        this.priceForm = '',
        this.desForm = ''

      requestAnimationFrame(() => {
        this.$refs.observer.reset();
      });
    },

    // POST
    async addNewProductForm(newProductForm) {
      try {
        const res = await fetch(this.url, {
          method: 'POST',
          headers: {
            'content-type': 'application/json'
          },
          body: JSON.stringify({
            name: newProductForm.name,
            band: newProductForm.band,
            price: newProductForm.price,
            des: newProductForm.des,
            file: newProductForm.file,
            // path: newProductForm.fileForm.name
          })
        })
        const data = await res.json()
        this.productInfo = [...this.productInfo, data]
      }
      catch (error) { console.log(`save failed: ${error}`) }
    },


    // dummyProductInCart(utaInfo) {
    //   this.editId = utaInfo.id
    //   this.nameForm = utaInfo.name
    //   this.bandForm = utaInfo.band
    //   this.priceForm = utaInfo.price
    //   this.desForm = utaInfo.des
    //   this.addDummyToCart({
    //     id: this.id,
    //     name: this.title,
    //     band: this.band,
    //     price: this.price,
    //     des: this.des
    //   })
    // },

    // async addDummyToCart(newDummyCartForm) {
    //   try {
    //     const res = await fetch(this.carturl, {
    //       method: 'POST',
    //       headers: {
    //         'content-type': 'application/json'
    //       },
    //       body: JSON.stringify({
    //         id: newDummyCartForm.id,
    //         name: newDummyCartForm.name,
    //         band: newDummyCartForm.band,
    //         price: newDummyCartForm.price,
    //         des: newDummyCartForm.des
    //       })
    //     })
    //     const data = await res.json()
    //     this.cartInfo = [...this.cartInfo, data]
    //   }
    //   catch (error) { console.log(`add dummy failed: ${error}`) }
    // },

    productInCart(utaInfo) {
      this.editId = utaInfo.id
      this.nameForm = utaInfo.name
      this.bandForm = utaInfo.band
      this.priceForm = utaInfo.price
      this.desForm = utaInfo.des


      this.addNewProductToCart({
        id: this.editid,
        name: this.nameForm,
        band: this.bandForm,
        price: this.priceForm,
        des: this.desForm,
        totalPrice: this.priceForm,
        quantity: this.defaultQuantity

      })
    },

    async addNewProductToCart(newProductToCart) {
      for (let i = 0; i < this.cartInfo.length; i++) {
        if (this.cartInfo[i].name == newProductToCart.name) {
          return this.editQuantity(this.cartInfo[i])
        }
      }
        try {
          const res = await fetch(this.carturl, {
            method: 'POST',
            headers: {
              'content-type': 'application/json'
            },
            body: JSON.stringify({
              id: newProductToCart.id,
              name: newProductToCart.name,
              band: newProductToCart.band,
              price: newProductToCart.price,
              des: newProductToCart.des,
              totalPrice: newProductToCart.totalPrice,
              quantity: newProductToCart.quantity

            })
          })
          const data = await res.json()
           console.log(`${data.id}`)
          // this.disabledbtn = true;
          // this.editQuantity(newProductToCart)
          // res.fetchclose()

          this.cartInfo = [...this.cartInfo, data]
        }
        catch (error) { console.log(`add to cart failed: ${error}`), console.log(`${this.cartInfo[0].name}`) }

      //***
    },
    async editQuantity(newQuantity) {
      newQuantity.quantity++
      try {
        const res = await fetch(`${this.carturl}/${newQuantity.id}`, {
          method: 'PUT',
          headers: {
            'content-type': 'application/json'
          },
          body: JSON.stringify({
            id: newQuantity.id,
            name: newQuantity.name,
            band: newQuantity.band,
            price: newQuantity.price,
            des: newQuantity.des,
            quantity: newQuantity.quantity
          })
        })
        const data = await res.json()
        this.cartInfo = this.cartInfo.map(cInfo => cInfo.id === newQuantity.id ?
          {
            ...cInfo,

            name: data.name,
            band: data.band,
            price: data.price,
            des: data.des,
            quantity: data.quantity
          } : cInfo
        )
      }
      catch (error) { console.log(`add quantity to cart failed: ${error}`), console.log(`${this.cartInfo[0].name}`) }

    },



    // GET
    // async getProductForm() {
    //   try {
    //     const res = await fetch(this.url)
    //     const getdata = await res.json()
    //     return getdata
    //   }
    //   catch (error) { console.log(`get product failed: ${error}`) }
    // },

    // async getCartForm() {
    //   try {
    //     const res = await fetch(this.carturl)
    //     const getcartdata = await res.json()
    //     return getcartdata

    //   }
    //   catch (error) { console.log(`get cart failed: ${error}`) }
    // },

    async getAccount() {
      try {
        const res = await fetch(this.accounturl)
        const getaccountdata = await res.json()
        return getaccountdata

      }
      catch (error) { console.log(`get account failed: ${error}`) }
    },

    // DELETE
    // async deleteProduct(deleteId) {
    //   try {
    //     await fetch(`${this.url}/${deleteId}`, {
    //       method: 'DELETE'
    //     })
    //     this.productInfo = this.productInfo.filter(uta => uta.id !== deleteId)
    //     this.reloadProduct()
    //   }
    //   catch (error) {
    //     console.log(`delete failed: ${error}`)
    //   }
    // },

    // async deleteCart(deleteCartId) {
    //   try {
    //     await fetch(`${this.carturl}/${deleteCartId}`, {
    //       method: 'DELETE'
    //     })
    //     this.cartInfo = this.cartInfo.filter(cInfo => cInfo.id !== deleteCartId)
    //     this.reloadCart()
    //   }
    //   catch (error) {
    //     console.log(`delete cart failed: ${error}`)
    //   }
    // },

    async deleteAccount(deleteAccountId) {
      try {
        await fetch(`${this.accounturl}/${deleteAccountId}`, {
          method: 'DELETE'
        })
        this.infoAccounts = this.infoAccounts.filter(a => a.id !== deleteAccountId)
        this.reloadAccount()
      }
      catch (error) {
        console.log(`delete account failed: ${error}`)
      }
    },

    // async reloadProduct() {
    //   this.productInfo = await this.getProductForm()
    // },

    // async reloadCart() {
    //   this.cartInfo = await this.getCartForm()
    // },

    async reloadAccount() {
      this.infoAccounts = await this.getAccount()
    },

    // EDIT
    showProduct(utaInfo) {
      this.inEditMode = true
      this.editId = utaInfo.id
      this.nameForm = utaInfo.name
      this.bandForm = utaInfo.band
      this.priceForm = utaInfo.price
      this.desForm = utaInfo.des
    },

    async editProduct(shinInfo) {
      try {
        const res = await fetch(`${this.url}/${shinInfo.id}`, {
          method: 'PUT',
          headers: {
            'content-type': 'application/json'
          },
          body: JSON.stringify({
            name: shinInfo.name,
            band: shinInfo.band,
            price: shinInfo.price,
            des: shinInfo.des
          })
        })
        const data = await res.json()
        this.productInfo = this.productInfo.map(uta => uta.id === shinInfo.id ?
          {
            ...uta,
            name: data.name,
            band: data.band,
            price: data.price,
            des: data.des
          } : uta
        )
        this.inEditMode = false
        this.editId = ''
        this.nameForm = ''
        this.bandform = ''
        this.priceForm = ''
        this.desForm = ''
      }
      catch (error) {
        console.log(`edit failed: ${error}`)
      }
    },
  },

  // GET-2
  async created() {
    // this.productInfo = await this.getProductForm()
    // this.cartInfo = await this.getCartForm()
    this.infoAccounts = await this.getAccount()

  }

}
</script>
