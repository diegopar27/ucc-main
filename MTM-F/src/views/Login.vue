<template>
  <v-app id="inspire">
    <v-content>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="8" lg="7">
            <v-card class="elevation-12">
              <v-window v-model="step">
                <v-window-item :value="1">
                  <v-col cols="12" md="8" lg="12">
                    <v-card-text class="mt-12">
                      <h1 class="text-center display-2" style="color: #03a9f4">Iniciar sesión</h1>
                      <br />
                      <h4 class="text-center mt-4">Brigadas de salud</h4>
                      <v-form>
                        <v-text-field label="Email" name="Email" prepend-icon="email" type="text" color="#03A9F4" v-model="usuario" />

                        <v-text-field
                          id="password"
                          label="Password"
                          name="password"
                          prepend-icon="lock"
                          type="password"
                          color="#03A9F4"
                          v-model="contraseña"
                        />
                      </v-form>
                      <h3 class="text-center mt-4">Olvidaste tu contraseña ?</h3>
                    </v-card-text>
                    <div class="text-center mt-3">
                      <v-btn rounded color="#03A9F4" dark v-on:click="login()">Iniciar sesión</v-btn>
                    </div>
                  </v-col>
                </v-window-item>
              </v-window>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import axios from "axios";
import { mapActions } from "vuex";
export default {
  data() {
    return {
      value1: "",
      value2: "",
      colorx: "#c72a75",
      colorx2: "#5252e8",
      usuario: "",
      contraseña: "",
    };
  },
  methods: {
    ...mapActions({
      LOGIN: "usuario/loginUsuario",
      GETHISTORIAS: "usuario/gethistorias",
    }),

    async login() {
      console.log("LOGIN");
      let data = {
        usuario: this.usuario,
        password: this.contraseña,
      };
      console.log(data);
      let res = await this.LOGIN({ data });
      if (res) {
        sessionStorage.usuario = JSON.stringify(res);
        return this.$router.push("/");
      }
    },

    // login() {
    //   axios
    //     .post("http://127.0.0.1:8000/api/user/lista", {
    //       usuario: this.usuario,
    //       contraseña: this.contraseña,
    //     })
    //     .then((resp) => console.log(resp))
    //     .catch((err) => console.log(err));
    // },
  },
  // created() {
  //   this.GETHISTORIAS();
  // },
};
</script>

<style></style>
