<template>
  <div>
    <Titulo texto="Terapeuta" />
    <div>
      <input type="text" placeholder="Nome do terapeuta" v-model="nome" @keyup.enter="addTerapeuta()" />
      <button class="btn btn-input" @click="addTerapeuta()">Adicionar</button>
    </div>

    <table>
      <thead>
        <th>Especialidades</th>
        <th>Nome completo</th>
        <th>CPF</th>
        <th>E-mail</th>
        <th>Telefone</th>
        <th>Opções</th>
      </thead>
      <tbody v-if="qtde > 0 ">
        <tr v-for="(terapeuta, index) in terapeutas" :key="index">
          <td>{{ terapeuta.especialidade.descricao }}</td>
          <td>{{ terapeuta.nomeCompleto }}</td>
          <td>{{ terapeuta.cpf }}</td>
          <td>{{ terapeuta.email }}</td>
          <td>{{ terapeuta.telefone1 }}</td>
          <td>{{ terapeuta.ativo }}</td>
          <td>
            <button class="btn btn_danger" @click="remover(terapeuta)">
              Remover
            </button>
          </td>
        </tr>
      </tbody>
      <tfoot v-else>
        Nenhum terapeuta encontrado
      </tfoot>
    </table>
  </div>
</template>

<script>
import Titulo from '../_share/Titulo.vue';
export default {
  components: {
    Titulo
  },
  data() {
    return {
      titulo: "Terapeuta",
      nome: "",
      terapeutas: [],
      qtde: 0
    };
  },
  methods: {
    getTerapeutas() {
      this.$http.get('https://localhost:44310/api/terapeutas')
        .then((res) => {
          this.terapeutas = res.data
          this.qtde = res.data.length

          //console.log(res.data)
        })
    },
    addTerapeuta() {
      let _terapeuta = {
        nome: this.nome,
      };
      this.terapeutas.push(_terapeuta);
      this.nome = "";
    },

    remover(terapeuta) {
      let indice = this.terapeutas.indexOf(terapeuta);
      this.terapeutas.splice(indice, 1);
    },

  },
  created() {
    this.terapeutas = this.getTerapeutas()

  },
  props: {}
};
</script>

<style scoped>
input {
  border: 0;
  padding: 20px;
  font-size: 14px;
  display: inline;
  margin-bottom: 15px;
  border-radius: 5px;
}

.btn-input {
  border: 0px;
  padding: 20px;
  margin-left: 5px;
  font-size: 1.3em;
  background-color: rgb(116, 115, 115);
}

.btn-input:houve {
  padding: 20px;
  margin: 0px;
  border: 0px;
}
</style>
