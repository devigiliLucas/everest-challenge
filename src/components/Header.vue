<template>
  <div class="nav-container">
    <div id="arrow">
      <i class="fa-solid fa-arrow-left click"></i>
    </div>
    <div id="title">
      <p>CADASTRO DE USUÁRIOS</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Header',
}
</script>

<style scoped>
  .nav-container{
    height: 7ch;
    width: 100%;
    background-color: rgb(224, 43, 87);
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    align-items: center;
  }

  #arrow{
    width: 43vw;
    color: white;
  }

  #title{
    width: 55vw;
    font-weight: bold;
    color: white;
  }

  .fa-arrow-left{
    font-size: 20px;
  }
</style>