<template>
  <div class="main-container">
    <div class="form-cont ">
      <h1 class="center title-form">Form</h1>

      <v-form ref="form" v-model="valid" lazy-validation>
        <v-text-field
          :rules="nameRules"
          v-model="name"
          label="Nombre completo*"
          variant="underlined"
          required
        ></v-text-field>

        <v-text-field
          v-model="email"
          :rules="emailRules"
          label="Correo electrónico*"
          variant="underlined"
          required
        ></v-text-field>
        <v-text-field
          variant="underlined"
          :counter="10"
          v-model="phone"
          :rules="phoneRules"
          label="Teléfono*"
          required
        ></v-text-field>
        <v-text-field
          variant="underlined"
          v-model="business"
          label="Empresa*"
          :rules="nameRules"
          required
        ></v-text-field>
        <v-text-field
          variant="underlined"
          v-model="job"
          label="Puesto"
        ></v-text-field>

        <v-btn
          :disabled="!valid"
          color="indigo darken-4"
          class="mr-4"
          @click="sendData"
          >Enviar
        </v-btn>

        <v-btn
          class="mr-4"
          @click="validate"
          >Validar
        </v-btn>
        <v-container>

        </v-container>
      </v-form>
    </div>
  </div>
</template>
<script>

// import axios from "axios";

export default {
  props: {
    nameReferred: String,
    method: Object,
  },
  data: () => ({
    showScript: false,
    num: 0,
    url: "hhh",
    dataUser: {},
    check_data: true,
    business: "",
    job: "",
    referred: "",
    phone: "",
    phoneRules: [
      (value) => !!value || "Por favor, ingresa un numero de teléfono.",
      (value) => (value || "").length === 10 || "Ingresa un número válido",
      (value) => {
        const pattern = /^[+]*[(]{0,1}[0-9]{1,4}[)]{0,1}[-\s\./0-9]*$/g;
        return pattern.test(value) || "Número invalido.";
      },
    ],

    valid: true,
    message: "holi",
    name: "",
    nameRules: [(v) => !!v || "Campo requerido"],
    email: "",
    emailRules: [
      (v) => !!v || "Por favor, ingresa un correo.",
      (v) => /.+@.+\..+/.test(v) || "El correo no es válido",
    ],
    select: null,
    checkbox: false,
  }),

  methods: {
    showSuccessAlert() {

      this.$swal.fire({
        icon: "success",
        title: "Validos",
        text: "Los datos han sido validados",
      });
    },
    validate() {
      this.$refs.form.validate();
    },
    reset() {
      this.$refs.form.reset();
      this.check_data = false;
      this.checkbox = false;

      setTimeout(() => {
        this.check_data = true;
        this.checkbox = true;
      }, 100);
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    },

    sendData() {
      const values = (this.dataUser = {
        date: new Date(),
        name: this.name,
        email: this.email,
        phone: this.phone,
        business: this.business,
        job: this.job,
        check: this.checkbox,
        check_data: this.check_data,
        referred: this.nameReferred,
      });
      console.log({values})
      this.showSuccessAlert()
      this.reset();



    }
  },
};
</script>

<style scoped>
.main-container {
  width: 100%;
  padding: 0 20px;
  padding-bottom: 60px;
}

.a-pdf {
  text-decoration: none;
  color: white;
  width: 100%;
  height: 100%;
}
.sp {
  margin-left: 6px !important;
}
.form-cont {
  padding: 15px;
  padding-bottom: 30px;
  width: 100%;
  border-radius: 15px;
  box-shadow: 0px 0px 2px 1px rgba(0, 0, 0, 0.1);
}
.link {
  text-decoration: underline;
  color: #282e68;
}

.title-form {
  margin-bottom: 10px;
  font-size: 18pt;
}

.left {
  text-align: left;
  color: rgba(0, 0, 0, 0.8);
}
.terms {
  color: rgba(51, 48, 48, 0.848);
  font-size: 13px;
  margin-left: -10px;
}

.center {
  text-align: center;
  color: rgba(0, 0, 0, 0.6);
}


</style>
