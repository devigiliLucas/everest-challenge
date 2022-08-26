<template>
  <div id="registers">
    <div id="container">
      <div id="title">
        <h2>Dados de contato</h2>
        <p>
          Lorem ipsum amet, consectetur adipiscing elit. Orci, volutpat in
          iaculis nec nibh nisl tellus.
        </p>
      </div>
      <form id="form">
        <div id="contents">
          <div id="name">
            <label class="label">Nome Completo</label>
            <input type="text" class="inpt" v-model="form.fullname" />
            <span v-if="nameError" class="error">Preencha este campo</span>
          </div>
          <div id="email">
            <label class="label">E-mail</label>
            <input type="text" class="inpt" v-model="form.email" />
            <span v-if="emailError" class="error">Digite um email válido</span>
          </div>
          <div id="confirm">
            <label class="label">Confirmar e-mail</label>
            <input type="text" class="inpt" v-model="form.confirm" />
            <span v-if="confirmError" class="error"
              >Os emails não coincidem</span
            >
          </div>
          <div id="cpf">
            <label class="label">Cpf</label>
            <input
              type="text"
              class="inpt"
              v-mask="cpfMask"
              v-model="form.cpf"
            />
            <span v-if="cpfError" class="error">Digite um cpf válido</span>
          </div>
          <div id="cell">
            <label class="label">Celular</label>
            <input
              type="text"
              class="inpt"
              v-mask="cellMask"
              v-model="form.phone"
            />
            <span v-if="cellError" class="error"
              >Preencha este campo corretamente</span
            >
          </div>
          <div id="date">
            <label class="label">Data de nascimento</label>
            <input type="date" class="inpt date" v-model="form.birthDate" />
            <span v-if="dateError" class="error">Preencha este campo</span>
          </div>
        </div>
      </form>
      <div id="texts">
        <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit.</p>
        <p>Mattis semper odio prtium vestibulum nulla</p>
      </div>
      <div id="selects">
        <div id="sms" class="selects">
          <input type="checkbox" v-model="form.sms" />
          <label>Email e sms</label>
        </div>
        <div id="whats" class="selects">
          <input type="checkbox" />
          <label>WhatsApp</label>
        </div>
      </div>
    </div>
    <footer id="footer">
      <button class="btn" id="save" @click="checkErrors, userCreate(form)">
        Salvar
      </button>
      <button class="btn" id="voltar">
        <router-link :to="{ name: 'users' }" class="link">Voltar</router-link>
      </button>
    </footer>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Register",
  data() {
    return {
      cpfMask: "###.###.###-##",
      cellMask: "(##) # ####-####",

      nameError: false,
      emailError: false,
      confirmError: false,
      cpfError: false,
      cellError: false,
      dateError: false,

      form: {
        fullname: "",
        email: "",
        confirm: "",
        cpf: "",
        phone: "",
        birthDate: "",
        sms: "",
      },
    };
  },
  methods: {
    errorName() {
      if (this.form.fullname == "") {
        this.nameError = true;
        return true;
      } else {
        return false, (this.nameError = false);
      }
    },

    errorEmail() {
      var reg = /^\w+([-+.']\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/;

      if (reg.test(this.form.email)) {
        return false, (this.emailError = false);
      } else {
        this.emailError = true;

        return true;
      }
    },

    errorConfirm() {
      if (this.form.email == this.form.confirm) {
        return false, (this.confirmError = false);
      } else {
        this.confirmError = true;
        return true;
      }
    },

    isCpf() {
      let rawCpf = this.form.cpf.replaceAll(".", "").replace("-", "");
      var Soma;
      var Resto;
      var i;
      Soma = 0;
      if (rawCpf == "00000000000") return false;

      for (i = 1; i <= 9; i++)
        Soma = Soma + parseInt(rawCpf.substring(i - 1, i)) * (11 - i);
      Resto = (Soma * 10) % 11;

      if (Resto == 10 || Resto == 11) Resto = 0;
      if (Resto != parseInt(rawCpf.substring(9, 10))) return false;

      Soma = 0;
      for (i = 1; i <= 10; i++)
        Soma = Soma + parseInt(rawCpf.substring(i - 1, i)) * (12 - i);
      Resto = (Soma * 10) % 11;

      if (Resto == 10 || Resto == 11) Resto = 0;
      if (Resto != parseInt(rawCpf.substring(10, 11))) return false;
    },

    errorCpf() {
      if (this.isCpf() == false) {
        this.cpfError = true;
        return true;
      } else {
        return false, (this.cpfError = false);
      }
    },

    errorCell() {
      if (this.form.phone == "") {
        this.cellError = true;
        return true;
      } else {
        return false, (this.cellError = false);
      }
    },

    errorData() {
      if (this.form.birthDate == "") {
        this.dateError = true;
        return true;
      } else {
        return false, (this.dateError = false);
      }
    },

    checkErrors() {
      if (
        !this.errorName() &&
        !this.errorEmail() &&
        !this.errorConfirm() &&
        !this.errorCpf() &&
        !this.errorCell() &&
        !this.errorData()
      ) {
        console.log("verificar false");
        return false;
      } else {
        console.log("verificar true");
        return true;
      }
    },

    async userCreate(form) {
      try {
        const newUser = {
          fullname: form.fullname,
          email: form.email,
          confirm: form.confirm,
          cpf: form.cpf,
          phone: form.phone,
          birthDate: form.birthDate,
          contacts: form.sms,
        };
        if (this.checkErrors()) {
          throw "formError";
        } else {
          const response = await axios.post("/api/users", newUser);
          this.$router.push({ name: "users" });
        }
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style scoped>
#registers {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

#container {
  width: 60vw;
}

#title {
  height: 10ch;
  width: 25vw;
  margin-top: 5%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

#form {
  height: 45ch;
  display: flex;
  align-items: center;
}

#contents {
  height: 40ch;
  width: 100%;
  display: grid;
  column-gap: 50px;
  grid-template-areas:
    "name name"
    "email confirm"
    "cpf fone"
    "date null";
}

#name {
  grid-area: name;
}

#email {
  grid-area: email;
}

#confirm {
  grid-area: confirm;
}

#cpf {
  grid-area: cpf;
}

#cell {
  grid-area: fone;
}

#date {
  grid-area: date;
}

.date {
  display: flex;
  flex-direction: row-reverse;
}

.inpt {
  height: 50%;
  width: 100%;
  border-radius: 5px;
  border: 1px solid black;
  padding-left: 10px;
  font-size: medium;
}

.label {
  margin-left: 15px;
  position: absolute;
  margin-top: -10px;
  background-color: white;
}

.error {
  color: red;
}

#texts {
  height: 10ch;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  font-weight: 700;
}

#selects {
  height: 15ch;
  width: 10%;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: flex-start;
}

.selects {
  width: 100%;
  display: flex;
  justify-content: space-between;
}

#footer {
  height: 10ch;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  border-top: 1px solid rgb(189, 189, 189);
}

.btn {
  height: 35px;
  width: 100px;
  border-radius: 10px;
  background-color: transparent;
  border: none;
}

#save {
  background-color: rgb(224, 43, 87);
  color: white;
}

#save:hover {
  background-color: rgb(199 18 62);
}

#voltar:hover {
  background-color: rgb(189, 189, 189);
}

.link {
  text-decoration: none;
  color: black;
}
</style>
