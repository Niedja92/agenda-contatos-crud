<template>
  <div>
    <h2>Lista de Contatos</h2>
    <ul>
      <li v-for="contato in contatos" :key="contato.id">
        <p>Nome: {{ contato.nome }}</p>
        <p>Email: {{ contato.email }}</p>
        <p>Telefone: {{ contato.telefone }}</p>
        <button>Editar</button>
        <button type="submit" @click="excluirContato(contato.id)">
          Excluir
        </button>
      </li>
    </ul>
    <button @click="carregarContatos">Carregar contatos</button>
  </div>
</template>

<script>
import CadastrarContato from "@/components/CadastrarContato.vue";
export default {
  name: "Contatos",
  components: {
    CadastrarContato,
  },
  data() {
    return {
      contatos: [],
    };
  },
  methods: {
    async carregarContatos() {
      await fetch("http://localhost:3000/contatos")
        .then((response) => response.json())
        .then((response) => {
          this.contatos = response; // usamos o this para mostrar estas informações na interface
          console.log(response);
        });

      // Pode ser feita como a função acima ou esta abaixo
      // async carregarContatos() {
      // const response = await fetch("http://localhost:3000/contatos");
      // const data = await response.json();
      // console.log(data);
      // this.contatos = data;
    },
    async excluirContato(id) {
      await fetch(`http://localhost:3000/contatos/${id}`, {
        method: "DELETE",
      })
        .then(() => {
          this.contatos = this.contatos.filter((contato) => contato.id !== id);
        })
        .catch((error) => {
          console.log("Erro ao tentar excluir contato:", error);
        });
    },
  },
  mounted() {
    this.carregarContatos();
  },
};
</script>

<style scoped>
ul {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 30px;
  margin: 20px;
}
</style>
