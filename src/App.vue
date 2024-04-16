<template>
  <div id="app">
    <CadastrarContato />
    <Contatos />
  </div>
</template>

<script>
import CadastrarContato from "@/components/CadastrarContato.vue";
import Contatos from "@/components/Contatos.vue";

export default {
  name: "App",
  components: {
    CadastrarContato,
    Contatos,
  },
};
</script>

<style>
* {
  font-family: "Poppins", sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  background-color: #b7b5b5;
}
</style>
