<template>
  <div id="app">
    <CadastrarContato />
    <Contatos />
  </div>
</template>

<script>
import Contatos from "@/components/Contatos.vue";
import CadastrarContato from "@/components/CadastrarContato.vue";

export default {
  name: "App",
  components: {
    CadastrarContato,
    Contatos,
  },
};
</script>

<style scoped>
* {
  font-family: "Poppins", sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
