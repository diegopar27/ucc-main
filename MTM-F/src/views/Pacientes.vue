<template>
  <div>
    <div>
      <div>
        <h1>Pacientes</h1>
        <div cols="12" md="4" lg="3">
          <v-btn color="success" @click="paciente.estado = true" dark large> Crear paciente </v-btn>
        </div>
      </div>
      <div>
        <!-- <div>
            <div cols="12" md="4" lg="3">
              <v-btn color="success" dark large> Consultar por numero ID </v-btn>
            </div>
          </div> -->

        <v-text-field cols="12" md="4" lg="3" v-model="search" label="Consultar por numero ID" class="purple-input" />

        <!-- :items="registros" -->
        <template>
          <v-data-table :search="search" :headers="headers" :items="pacientes" item-key="id" :items-per-page="5" class="elevation-1"></v-data-table>
        </template>
      </div>
    </div>
    <PACIENTE :paciente="paciente"></PACIENTE>
  </div>
</template>
<script>
import popapPaciente from "../components/PCT.vue";
import axios from "axios";
import { Global } from "../global";
import { mapActions } from "vuex";

export default {
  components: {
    PACIENTE: popapPaciente,
  },
  data: () => ({
    search: "",
    headers: [
      {
        text: "ID",
        align: "center",
        sortable: false,
        value: "id",
      },
      {
        text: "Nombre",
        align: "center",
        sortable: false,
        value: "Name",
      },
      {
        text: "Apellido",
        align: "center",
        sortable: false,
        value: "Surname",
      },
      {
        text: "Tipo doc.",
        align: "center",
        sortable: false,
        value: "type_identification",
      },
      {
        text: "Numero doc.",
        align: "center",
        sortable: false,
        value: "identification_number",
      },
      {
        text: "Numero celular",
        align: "center",
        sortable: false,
        value: "Phone",
      },
      {
        text: "Dirección",
        align: "center",
        sortable: false,
        value: "Direction",
      },
      {
        text: "Genero",
        align: "center",
        sortable: false,
        value: "gender",
      },
      {
        text: "EPS",
        align: "center",
        sortable: false,
        value: "Eps",
      },
      {
        text: "Correo",
        align: "center",
        sortable: false,
        value: "email",
      },
      {
        text: "Fecha de nacimiento",
        align: "center",
        sortable: false,
        value: "date_of_birth",
      },
    ],
    paciente: {
      estado: false,
    },
    pacientes: [],
  }),
  async mounted() {
    this.pacientes = await this.getPacientes();
    console.log("array pacientes", this.pacientes);
    this.getServicios();
  },
  methods: {
    ...mapActions({
      getPacientes: "pacientes_api/getPacientes",
      getPaciente: "paciente/getPaciente",
    }),
    async obtenerPaciente() {
      const id = this.search;
      let res = await this.getPaciente({ id });
    },

    getServicios() {
      let config = {
        // Headers:{
        //   'token': Global.token
        // }
      };
      axios.get(Global.url + "/api/Patients/listpatients/").then((res) => {
        console.log("estoy en metodo get pacientes", res.status);
        if (res.status == 200) {
          this.historia_cli = res.data;
          console.log((this.historia_cli.id = "1"));
        } else {
          alert("no se pudo conectar");
        }
      });
    },
  },
};
</script>
<style scoped>
.border {
  border-left: 4px solid #0ba518;
}
</style>
