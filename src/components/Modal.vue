<template>
  <div id="modal">
    <div id="header">
      <div id="title">
        <p class="title">Detalhes do usuário</p>
      </div>
      <div id="headerBtn">
        <button class="btn click" @click="closeModal">
          <i class="btn-ic-close fa-regular fa-x"></i>
        </button>
      </div>
    </div>
    <div id="contents">
      <div id="rightColumn">
        <div id="cel">
          <label>Celular</label>
          <p class="dados">{{ dados.phone | VMask("(##) # ####-####") }}</p>
        </div>
        <div id="ctt">
          <label>Contato</label>
          <div id="contact">
            <div id="cttSms" v-if="contact">
              <i class="fa-solid fa-message"></i>
              <p class="dados">Sms e email</p>
            </div>
            <div id="cttWhatsApp" v-else>
              <i class="fa-brands fa-whatsapp"></i>
              <p class="dados">WhatsApp</p>
            </div>
          </div>
        </div>
        <div id="email">
          <label>Email</label>
          <p class="dados">{{ dados.email }}</p>
        </div>
      </div>
      <div id="leftColumn">
        <div id="cpf">
          <label>CPF</label>
          <p class="dados">{{ dados.cpf | VMask("###.###.###-##") }}</p>
        </div>
        <div id="name">
          <label>Name</label>
          <p class="dados">{{ dados.fullname }}</p>
        </div>
        <div id="date">
          <label>Data</label>
          <p class="dados">{{ dados.birthDate | VMask("####/##/##") }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: {
    dados: {
      type: Object,
    },
  },
  computed: {
    contact() {
      if (this.dados.contacts) {
        return true;
      } else {
        return false;
      }
    },
  },
  methods: {
    closeModal() {
      this.$emit("closeModal");
    },
  },
};
</script>

<style scoped>
#modal {
  height: 66vh;
  width: 35vw;
  background-color: white;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: absolute;
  top: 50%;
  left: 50%;
  right: -50%;
  transform: translate(-50%, -50%);
  box-shadow: 0px 0px 1px 1100px rgba(0, 0, 0, 0.5);
}

#header {
  height: 10vh;
  width: 30vw;
  display: grid;
  grid-template-areas: "title button";
  align-content: center;
  align-items: center;
  justify-items: end;
}

.btn {
  background-color: transparent;
  border: none;
}

.btn:hover {
  transform: scale(1.3);
  transition: all 0.25s;
  color: red;
}

#contents {
  height: 50vh;
  width: 30vw;
  border: 2px dashed gray;
  display: flex;
  flex-direction: row-reverse;
  justify-content: center;
}

label {
  color: gray;
}

.dados {
  font-weight: 700;
}

#rightColumn {
  width: 12vw;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

#leftColumn {
  width: 12vw;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

#cttWhatsApp {
  display: flex;
  justify-content: space-between;
  width: 5vw;
}

#cttSms {
  display: flex;
  justify-content: space-between;
  width: 5.8vw;
}
</style>
