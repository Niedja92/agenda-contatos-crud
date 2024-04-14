<template>
  <div>
    <h2>Cadastrar Novo Contato</h2>
    <form @submit.prevent="addContato">
      <label for="nome">Nome:</label>
      <input type="text" name="nome" v-model="novoContato.nome" required />
      <label for="email">Email</label>
      <input type="text" name="email" v-model="novoContato.email" required />
      <label for="telefone">Telefone</label>
      <input
        type="text"
        name="telefone"
        v-model="novoContato.telefone"
        required
      />

      <button type="submit">Adicionar</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "CadastrarContato",
  data() {
    return {
      contatos: [],
      novoContato: {
        nome: "",
        email: "",
        telefone: "",
      },
    };
  },
  mounted() {
    this.addContato();
  },
  methods: {
    async addContato() {
      await fetch("http://localhost:3000/contatos", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(this.novoContato),
      })
        .then((response) => response.json())
        .then((contato) => {
          this.contatos.push(contato); // adicionar os elementos aos campos
          // limpa os campos após adicionar Novo Contato
          (this.novoContato.nome = ""),
            (this.novoContato.email = ""),
            (this.novoContato.telefone = "");
        })
        .catch((error) => {
          console.log("Erro ao tentar adicionar contato:", error);
        });
    },
  },
};
</script>

<style scoped>
form,
h2 {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
