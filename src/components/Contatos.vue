<template>
  <div>
    <h2>Lista de Contatos</h2>
    <div>
      <ul>
        <li v-for="contato in contatos" :key="contato.id">
          <p>Nome: {{ contato.nome }}</p>
          <p>Email: {{ contato.email }}</p>
          <p>Telefone: {{ contato.telefone }}</p>
          <div class="btn">
            <button>Editar</button>
            <button @click="excluirContato(contato.id)">Excluir</button>
          </div>
        </li>
      </ul>
    </div>
    <div class="btn-div">
      <button class="btn-carregar" @click.prevent="carregarContatos">
        Carregar contatos
      </button>
    </div>
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
  mounted() {
    this.carregarContatos();
  },
  methods: {
    // 'GET'
    async carregarContatos() {
      await fetch("http://localhost:3000/contatos")
        .then((r) => r.json())
        .then((r) => {
          this.contatos = r; // usamos o this para mostrar estas informações na interface
          console.log(r);
        });
    },
    //'DELETE'
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
      this.carregarContatos(); // após executar o o excluirContato, atualiza os permanecem
    },
  },
};
</script>

<style scoped>
h2 {
  display: flex;
  justify-content: center;
  padding: 20px;
}
ul {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 30px;
  margin: 20px;
  list-style-type: none;
}

li {
  border: 1px solid #000;
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  align-items: left;
  background-color: #e5e1e1;
  padding: 10px;
  width: 400px;
}

p {
  padding: 5px;
}

.btn {
  display: flex;
  justify-content: center;
  padding: 10px;
}
button {
  margin: 0 10px;
  cursor: pointer;
  padding: 5px;
  border: 1px solid #1233eb;
  border-radius: 4px;
  color: #1233eb;
}

button:hover,
button:focus {
  background: #b9c0ed;
}

.btn-carregar:hover,
.btn-carregar:hover {
  background: #576ae3;
  color: #000;
  border: none;
}

.btn-carregar {
  font-size: 16px;
  margin-bottom: 50px;
}

.btn-div {
  display: flex;
  justify-content: center;
  padding: 30px;
}
</style>
