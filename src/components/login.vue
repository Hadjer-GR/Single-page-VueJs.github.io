<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <section class="vh-100">
    <div class="container-fluid h-custom">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col-md-9 col-lg-6 col-xl-5">
          <img
            src="../../public/images/back5.jpg"
            class="img-fluid"
            alt="Sample image"
          />
        </div>
        <div class="col-md-8 col-lg-6 col-xl-4 offset-xl-1">
          <form @submit.prevent="login()">
            <div
              class="d-flex flex-row align-items-center justify-content-center justify-content-lg-start"
            >
              <p
                class="lead fw-normal mb-0 me-3"
                style="
                  text-align: center;
                  font-size: 1.2em !important;
                  font-weight: 600;
                "
              >
                Sign in
              </p>
            </div>

            <div class="divider d-flex align-items-center my-4">
              <!-- <p class="text-center fw-bold mx-3 mb-0">Or</p> -->
            </div>

            <!-- Email input -->
            <div class="form-outline mb-4">
              <label class="form-label" for="form3Example3"
                >Email address</label
              >
              <input
                type="email"
                id="form3Example3"
                class="form-control form-control-lg"
                placeholder="Enter a valid email address"
                v-model.lazy.trim="email"
              />
            </div>

            <!-- Password input -->
            <div class="form-outline mb-3">
              <label class="form-label" for="form3Example4">Password</label>
              <input
                type="password"
                id="form3Example4"
                class="form-control form-control-lg"
                placeholder="Enter password"
                v-model.lazy="password"
                required
              />
            </div>
            <p class="link-danger" style="color: red !important;">{{ error }}</p>
            <div class="d-flex justify-content-between align-items-center">
              <!-- Checkbox -->
              <div class="form-check mb-0">
                <input
                  class="form-check-input me-2"
                  type="checkbox"
                  value=""
                  id="form2Example3"
                />
                <label class="form-check-label" for="form2Example3">
                  Remember me
                </label>
              </div>
            </div>

            <div class="text-center text-lg-start mt-4 pt-2">
              <button
                type="submit"
                class="btn btn-primary btn-lg"
                style="padding-left: 2.5rem; padding-right: 2.5rem"
              >
                Login
              </button>
              <p class="small fw-bold mt-2 pt-1 mb-0">
                Don't have an account?
                <router-link to="/register" class="link-danger"
                  >Register</router-link
                >
              </p>
            </div>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>


<script>
import axios from "axios";

export default {
  data() {
    return {
      email: "",
      password: "",
      error: "",
    };
  },
  methods: {
    async login() {
      const user = {
        email: this.email,
        password: this.password,
      };
      axios
        .post("login", user)
        .then((resp) => {
          this.error = "";
          console.log(resp.data)
          localStorage.setItem("token", resp.data.token);
          this.$router.push("/news");
        })
        .catch((err) => {
          console.log(err);
          this.error = "uncorrect password";
        });
    },
  },
};
</script>

<style scoped>
.container-fluid {
  margin-top: 10% !important;
}

.btn-lg {
  background-color: rgba(254, 187, 0) !important;
  border: none !important;
  transition: all 0.2s;
}
.btn-lg:hover {
  transform: scale(1.1);
}
#form2Example3:checked {
  background-color: rgba(254, 186, 0, 0.633) !important;
  border: none !important;
}
.divider:after,
.divider:before {
  content: "";
  flex: 1;
  height: 1px;
  background: #eee;
}
.h-custom {
  height: calc(100% - 73px);
}
@media (max-width: 450px) {
  .h-custom {
    height: 100%;
  }
}
</style>