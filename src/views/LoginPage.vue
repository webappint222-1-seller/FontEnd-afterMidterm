<template>
  <div class="home">
    <Navbar />
    <v-container class="flex justify-center pt-10">
      <v-card class="pa-4 text-white" dark>
        <login @login-user="confirmLogin" />
      </v-card>
    </v-container>
  </div>
</template>
  
  <script>
import Navbar from "@/components/Navbar.vue";
import Login from "@/components/Login.vue";


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
    Login,
    // Member
  },
  methods: {
    async fetchEmailPassword() {
      try {
        const res = await fetch(this.url);
        const data = await res.json();
        return data;
      } catch (error) {
        console.log(error);
      }
    },
    // validateEmailPassword(EmailPassword) {
    //   console.log(EmailPassword.email);

    //   this.infoAccounts = this.infoAccounts.filter(
    //     (info) =>
    //       info.email == EmailPassword.email &&
    //       info.password == EmailPassword.password
    //   );
    //   if (this.infoAccounts.length !== 0) {
    //     if (
    //       this.infoAccounts[0].email == EmailPassword.email &&
    //       this.infoAccounts[0].password == EmailPassword.password
    //     ) {
    //       alert("Login Success");
    //       this.login = true;
    //       this.$router.push('/');
    //     }
    //   } else {
    //     alert("Login fail");
    //     location.reload();
    //   }
    //   console.log(this.infoAccounts);
    // },




    confirmLogin(EmailPassword) {
      console.log(`email: ${EmailPassword.email}`)

      // this.$swal.fire({
      // title: 'Are you sure?',
      // text: "You won't be able to revert this!",
      // icon: 'warning',
      // showCancelButton: true,
      // confirmButtonColor: '#3085d6',
      // cancelButtonColor: '#d33',
      // confirmButtonText: 'Confirm'
      // }).then((result) => {
      // if (result.isConfirmed) {
      this.infoAccounts = this.infoAccounts.filter(
        (info) =>
          info.email == EmailPassword.email &&
          info.password == EmailPassword.password
      );
      if (this.infoAccounts.length !== 0) {
        if (
          this.infoAccounts[0].email == EmailPassword.email &&
          this.infoAccounts[0].password == EmailPassword.password
        ) {

          // this.$swal.fire({
          // title: 'Login success!',
          // text: 'Your has been login.',
          // icon: 'success'
          // })

          const Toast = this.$swal.mixin({
            toast: true,
            position: 'top-end',
            showConfirmButton: false,
            timer: 2000,
            timerProgressBar: true,
            didOpen: (toast) => {
              toast.addEventListener('mouseenter', this.$swal.stopTimer)
              toast.addEventListener('mouseleave', this.$swal.resumeTimer)
            }
          })

          Toast.fire({
            icon: 'success',
            title: 'Login is successfully'
          })
          this.$router.push('/');


          // location.reload();
        }
      } else {
        this.$swal.fire({
          // title: '<span class= "text-white"> Login failed! </span>',            
          // text: '<span class= "text-white"> Your email or password wrong please try again. </span>',              
          title: 'Login failed!',
          text: 'Your email or password wrong please try again.',
          icon: 'error',
          footer: '<a href="/registerpage" class= "font-bold text-lightpink"> Need to register? </a>',
          // background: 'black'            


        })

      }
      // }
      // })

    },

  },
  async created() {
    this.infoAccounts = await this.fetchEmailPassword();
  },
};
</script>