<template>
  <div>
    <h2>Cadastrar Novo Contato</h2>
    <form @submit.prevent="addContato">
      <label for="nome">Nome</label>
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
    // 'GET'
    async carregarContatos() {
      const request = await fetch("http://localhost:3000/contatos");
      const data = await request.json();
      console.log(data);
    },

    // 'POST'
    async addContato() {
      await fetch("http://localhost:3000/contatos/", {
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
h2 {
  padding-bottom: 20px;
}
div {
  padding: 30px;
}

form,
h2 {
  display: flex;
  flex-direction: column;
  align-items: center;
}

label {
  padding: 10px;
}

input {
  border: none;
  border-radius: 5px;
  padding: 10px;
  width: 300px;
  outline: none;
}

button {
  cursor: pointer;
  margin-top: 20px;
  padding: 10px;
  width: 320px;
  border: none;
  border-radius: 5px;
  background-color: #1233eb;
  color: #fff;
  transition: 1s;
  font-size: 16px;
}

button:hover,
button:focus {
  background: #4760ed;
}
</style>
