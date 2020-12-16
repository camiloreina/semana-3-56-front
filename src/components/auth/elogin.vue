<template>
  <div id="contenedor" class="border border-secondary rounded p-4">

    <div class="md-form form-group w-75">
      <div class="input-group">
        <i class="fa fa-user prefix"></i>
        <input
          v-model="login.email"
          type="email"
          class="form-control" 
          id="exampleInputEmail1"
          aria-describedby="emailHelp"
          placeholder="Ingrese correo"
        >
      </div>
    </div>


    <div class="md-form form-group w-75">
      <div class="input-group">
        <i class="fa fa-key prefix"></i>
        <input
          v-model="login.password"
          type="password"
          class="form-control"
          id="exampleInputPassword1"
          placeholder="Password"
        >
      </div>
    </div>

    <button 
    @click.prevent ="LoginUser"
    type="submit" 
    class="btn btn-dark active">Ingresar</button>

  </div>
</template>

<script>
export default {
  name: "elogin",
  data() {
    return{
        login:{
            email:'',
            password: ''
        }
    };
  },
  methods: {

      async LoginUser(){
          try{
            let response = await this.$http.post('/api/usuario/login', this.login)
            console.log(response.data);
            let token = response.data.tokenReturn;
            let user = response.data.user;

            localStorage.setItem('jwt', token)
            localStorage.setItem('user',JSON.stringify(user));
            if(token){
                this.$router.push('/home')
            }
            else{
                console.log(err.response)
            }
          }
          catch{}
      }
  }
};
</script>
<style scoped>
#contenedor {
  background-color: rgb(210, 210, 216);
}

</style>