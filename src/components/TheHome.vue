<template>

  <div>










    JULIAN
    
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarTogglerDemo01"
          aria-controls="navbarTogglerDemo01"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarTogglerDemo01">
          <form class="d-flex">
            <button
              class="btn btn-outline-success"
              type="submit"
              @click.prevent="logOut"
            >
              Salir
            </button>
          </form>
        </div>
      </div>
    </nav>
    <div class="container">
      <p>
        {{ user.name }}
      </p>
      <p>
        {{ user.email }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {
    gerUserDetails() {
        let user = localStorage.getItem('user');
        let token = localStorage.getItem('jwt');
        if(token){
            this.user = JSON.parse(user);
        }
    },
    logOut() {
      localStorage.removeItem("jwt");
      localStorage.removeItem("user");
      this.$router.push("/");
    },
  },
  created() {
    this.gerUserDetails();
  },
};
</script>
