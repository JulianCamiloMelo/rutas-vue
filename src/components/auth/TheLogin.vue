<template>
  <div class="container mt-5">
    <form class="Fondo">
      <div class="mb-5" autocomplete="false">
        <div class="row justify-content-center">
          <div class="col-4">
            <h1>INICIAR SESIÓN</h1>
          </div>
          <div class="col-5">
            <br />

            <label for="exampleInputEmail1" class="form-label"
              >Ingrese su Correo electrónico:</label
            >

            <div class="input-group flex-nowrap">
              <span class="input-group-text" id="addon-wrapping">@</span>

              <input
                v-model="login.email"
                type="email"
                class="form-control"
                id="exampleInputEmail1"
                aria-describedby="emailHelp"
              />
            </div>

            <div class="mb-4">
              <br />
              <label for="exampleInputPassword1" class="form-label"
                >Ingrese su Contraseña:</label
              >
              <input
                v-model="login.password"
                type="password"
                class="form-control"
                id="exampleInputPassword1"
              />

              <br />

              <button
                @click.prevent="loginUser"
                type="submit"
                class="btn btn-primary btn-lg"
              >
                Inicio de Sesión
              </button>
            </div>
          </div>
        </div>
      </div>
    </form>
    <pre class="fondo azul">
        {{ login }}
    </pre>
  </div>
</template>

<script>
import swal from "sweetalert";

export default {
  name: "TheLogin",
  data() {
    return {
      login: {
        email: "",
        password: "",
      },
    };
  },
  methods: {
    async loginUser() {
      try {
        let response = await this.$http.post("/api/auth/signin", this.login);
        console.log(response.data);
        let token = response.data.accessToken;
        let user = response.data.user;

        localStorage.setItem("jwt", token);
        localStorage.setItem("user", JSON.stringify(user));

        if (token) {
          swal("Exito!!", "Login Correcto", "success");
          this.$router.push("/home");
        }
      } catch {
        swal("Error!", "Algo salio mal", "error");
      }
    },
  },
};
</script>

<style>
.Fondo {
  background-color: rgb(156, 204, 223);
}
</style>