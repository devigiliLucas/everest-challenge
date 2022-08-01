<template>
  <header>
    <div id="btnNav">
      <div id="btn">
        <section id="btnNavRegister">
          <button
            @click="btnCadastro"
            class="button btnClickCadastro"
            v-if="cadastroClick"
          >
            <router-link :to="{ name: 'register' }" class="click clickBtn"
              >Cadastro</router-link
            >
          </button>

          <button @click="rawBntCadastro" class="button" v-else>
            <router-link :to="{ name: 'register' }" class="rawBtnNav click"
              >Cadastro</router-link
            >
          </button>
        </section>

        <section id="btnNavUsers">
          <Button
            @click="bntListagem"
            class="button btnClickListagem"
            v-if="listagemClick"
          >
            <router-link :to="{ name: 'users' }" class="click clickBtn"
              >Listagem</router-link
            >
          </Button>

          <Button @click="rawBntListagem" class="button" v-else>
            <router-link :to="{ name: 'users' }" class="rawBtnNav click"
              >Listagem</router-link
            >
          </Button>
        </section>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "NavBar",
  data() {
    return {
      cadastro: "",
      listagem: "",

      cadastroClick: false,
      listagemClick: true,
    };
  },
  methods: {
    rawBntCadastro() {
      this.cadastroClick = true;
      this.listagemClick = false;
    },
    rawBntListagem() {
      this.cadastroClick = false;
      this.listagemClick = true;
    },
  },
};
</script>

<style scoped>
header {
  height: 15ch;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: center;
}

.button {
  background-color: transparent;
  height: 5ch;
  width: 10vw;
  border: none;
}

.btnClickCadastro {
  font-weight: 700;
  border-bottom: 3px solid black;
}

.btnClickListagem {
  font-weight: 700;
  border-bottom: 3px solid black;
}

#btn {
  width: 15vw;
  height: 5ch;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}

.rawBtnNav {
  height: 74px;
  width: 140px;
  font-size: 17px;
  background-color: transparent;
  border: transparent;
  text-decoration: none;
  color: black;
}

.clickBtn {
  text-decoration: none;
  color: black;
}

.btnNav {
  height: 74px;
  width: 140px;
  font-size: 17px;
  background-color: pink;
  border: transparent;
}

#btnCadastro {
  width: 40vw;
  display: flex;
  justify-content: end;
}
</style>
