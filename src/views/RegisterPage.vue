<template>
  <div class="home">
    <Navbar />
    <v-container class="flex justify-center pt-10">
      <v-card class="pa-4 text-white" dark >
        <register @register-user="confirmRegis" />
        <!-- <v-card>
        <button @click="confirm()">
          test
        </button>
        </v-card>-->
      </v-card>
    </v-container>
  </div>
</template>
  
  <script>
import Navbar from "@/components/Navbar.vue";
import Register from "@/components/Register.vue";


export default {
  name: "Home",
  data() {
    return {
      url: " http://localhost:5000/infoAccounts",
      infoAccounts: [],
    };
  },
  components: {
    Navbar,
    Register,

    // Member
  },
  methods: {

    async fetchinfoRegister() {
      try {
        const res = await fetch(this.url);
        const data = await res.json();
        return data;
      } catch (error) {
        console.log(error);
      }
    },

    async addNewRegister(infoRegister) {
      // this.infoAccounts = this.infoAccounts.filter(
      //   (info) =>
      //     info.email == infoRegister.email
      //   // info.password == infoRegister.password
      // );
      // if (this.infoAccounts.length !== 0) {
      //   if (
      //     this.infoAccounts[0].email == infoRegister.email
      //   ) {
      //     // this.$alert("Register Fail: this user have used");
      //     location.reload();
      //   }
      // } else {
      // this.$alert("Registe success");
      const res = await fetch(this.url, {
        method: 'POST',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify({
          email: infoRegister.email,
          password: infoRegister.password,
          name: infoRegister.name,
          phone: infoRegister.phone,
          date: infoRegister.date,
          address: infoRegister.address
        })
      })
      const data = await res.json()
      this.infoResults = [...this.infoResults, data]
      // this.$alert("Registe success");

    
    },

     confirmRegis(infoRegister) {
       console.log(`email: ${infoRegister.email}`)
      this.$swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Confirm'
      }).then((result) => {
        if (result.isConfirmed) {
          this.infoAccounts = this.infoAccounts.filter(
            (info) =>
              info.email == infoRegister.email
            // info.password == infoRegister.password
          );
          if (this.infoAccounts.length !== 0) {
            if (
              this.infoAccounts[0].email == infoRegister.email
            ) {
               this.$swal.fire(
              'Register failed!',
              'Your email has used please try again.',
              'error'
            )             
              // location.reload();
            }
          } else {
            this.addNewRegister(infoRegister)
            this.$swal.fire(
              'Registered!',
              'Your has been registered.',
              'success'
            )
          }
        }
      })
    },

    
    // validateInfo(infoRegister) {

    //   this.infoAccounts = this.infoAccounts.filter(
    //     (info) =>
    //       info.username == infoRegister.username &&
    //       info.password == infoRegister.password
    //   );
    //   if (this.infoAccounts.length !== 0) {
    //     if (
    //       this.infoAccounts[0].username == infoRegister.username
    //     ) {
    //       alert("Register Fail: this user have used");
    //       location.reload();
    //     }
    //   } else {
    //     alert("Registe success");

    //   }
    //   console.log(this.infoAccounts);
    // },
    // this.$confirm("Are you sure?").then(() => {

  },

  async created() {
    this.infoAccounts = await this.fetchinfoRegister();
  },
};

</script>

