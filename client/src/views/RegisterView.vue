<template>
  <section class="vh-100" style="background-color: #eee">
    <div class="container h-100">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col-lg-12 col-xl-11">
          <div class="card text-black" style="border-radius: 25px">
            <div class="card-body p-md-5">
              <div class="row justify-content-center">
                <div class="col-md-10 col-lg-6 col-xl-5 order-2 order-lg-1">
                  <p class="text-center h1 fw-bold mb-5 mx-1 mx-md-4 mt-4">
                    Sign up
                  </p>

                  <form class="mx-1 mx-md-4">
                    <div class="d-flex flex-row align-items-center mb-4">
                      <i class="fas fa-envelope fa-lg me-3 fa-fw"></i>
                      <div class="form-outline flex-fill mb-0">
                        <input
                          v-model="input.email"
                          type="email"
                          class="form-control"
                        />
                        <label class="form-label" for="form3Example3c"
                          >Email</label
                        >
                      </div>
                    </div>

                    <div class="d-flex flex-row align-items-center mb-4">
                      <i class="fas fa-lock fa-lg me-3 fa-fw"></i>
                      <div class="form-outline flex-fill mb-0">
                        <input
                          v-model="input.password"
                          type="password"
                          class="form-control"
                        />
                        <label class="form-label" for="form3Example4c"
                          >Password</label
                        >
                      </div>
                    </div>
                    <div class="text-center text-lg-start mt-4 pt-2">
                      <button
                        type="button"
                        class="btn btn-primary btn-lg"
                        @click="handleRegister"
                      >
                        Register
                      </button>
                      <p class="small fw-bold mt-2 pt-1 mb-0">
                        Already have an account?
                        <a href="#!" class="link-danger" @click.prevent="login"
                          >Login</a
                        >
                      </p>
                    </div>
                  </form>
                </div>
                <div
                  class="col-md-10 col-lg-6 col-xl-7 d-flex align-items-center order-1 order-lg-2"
                >
                  <img
                    src="https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-registration/draw1.webp"
                    class="img-fluid"
                    alt="Sample image"
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { mapActions } from "pinia";
import { useCustomStore } from "../stores/index";
export default {
  data() {
    return {
      input: {
        email: "",
        password: "",
      },
    };
  },
  methods: {
    login() {
      this.$router.push("/login");
    },
    ...mapActions(useCustomStore, ["register"]),
    async handleRegister() {
      try {
        const result = await this.register(
          this.input.email,
          this.input.password
        );
        // console.log(result, ">>>>????");
        if (result.message) {
          throw { message: result };
        } else {
          Swal.fire("Cool!", "You have registered succesfully!", "success");
          this.$router.push("/login");
        }
      } catch (error) {
        // console.log(error);
        // console.log(error.message.response.data.errors, "<><><><><");
        console.log(error);
      }
    },
  },
};
</script>
