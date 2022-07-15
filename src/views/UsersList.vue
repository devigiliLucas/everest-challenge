<template>
  <div id="userList">
    <div class="container">
      <div id="header">
        <p class="headerCpf margin">CPF</p>
        <p class="headerNome margin">NOME COMPLETO</p>
      </div>
      <div id="paginacao">
        <div id="lista">
          <ul v-for="user in currentItens" :key="user.message">
            <div id="cpf">
              <li class="cpf margin">
                {{ user.cpf | VMask(mask) }}
              </li>
            </div>
            <div id="nome">
              <li class="name margin">{{ user.fullname }}</li>
            </div>
            <div id="hidden">
              <li class="hidden" @click="openModal(user)">
                <i class="fa-solid fa-eye click"></i>
              </li>
            </div>
          </ul>
        </div>
      </div>
    </div>

    <jw-pagination
      :labels="customLabels"
      :pageSize="10"
      :maxPages="4"
      :items="dataUsers"
      @changePage="onChangePage"
    ></jw-pagination>

    <Modal
      v-show="modal"
      id="modal"
      @closeModal="closeModal"
      :dados="dadosPessoais"
    />
  </div>
</template>

<script>
import axios from "axios";
import Modal from "../components/Modal.vue";

const customLabels = {
  first: "",
  last: "",
  previous: "<",
  next: ">",
};

export default {
  name: "UsersList",
  data() {
    return {
      url: "http://localhost:8080/api/users",
      dataUsers: [],
      currentItens: [],
      customLabels,
      mask: "###.###.###-##",
      modal: false,
      dados: {},
      dadosPessoais: {},
    };
  },
  components: {
    Modal,
  },
  
  methods: {
    onChangePage(currentItens) {
      this.currentItens = currentItens;
    },

    openModal(user) {
        this.modal = true
        this.dadosPessoais = user
    },

    closeModal() {
      this.modal = false;
    },
  },

  async mounted() {
    const response = await axios.get(this.url);
    this.dataUsers = response.data.users;
  },
};
</script>

<style scoped>
#userList {
  height: 65ch;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

::v-deep .page-number {
  color: gray !important;
}

::v-deep .active {
  color: black !important;
  font-weight: 700;
}

.container {
  height: 57ch;
  width: 60vw;
  border-bottom: 1px solid rgb(189, 189, 189);
  display: grid;
  grid-template-columns: 30fr 70fr 10fr;
  grid-template-rows: 5vh 5vh 5vh 5vh 5vh 5vh 5vh 5vh 5vh 5vh;
  grid-template-areas: "header header header";
}

#header {
  font-weight: 700;
  grid-area: header;
  border-top: 1px solid rgb(189, 189, 189);
  border-bottom: 1px solid rgb(189, 189, 189);
  display: grid;
  align-items: center;
  grid-template-columns: 30fr 80fr;
}

#cpf {
  grid-area: cpf;
}

#nome {
  grid-area: nome;
}

#hidden {
  grid-area: hiden;
}

#paginacao {
  height: 450px;
  width: 60vw;
}

#lista {
  width: 60vw;
}

ul {
  display: flex;
  align-items: center;

  display: grid;
  grid-template-columns: 30fr 70fr 10fr;
  grid-template-rows: 3vh;
  grid-template-areas:
    "header header header"
    "cpf nome hiden";
}
ul li {
  font-size: 13px;
  list-style-type: none;
}

.cpf {
  width: 260px;
}

.margin {
  margin-left: 20px;
}

.fa-eye:hover {
  transform: scale(1.3);
  transition: all 0.25s;
}
</style>
