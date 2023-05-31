<template>
  <div>
    <div class="col-12">
      <div class="card-plain">
        <div class="table-full-width table-responsive">
          <table class="table">
            <thead>
              <tr>
                <th v-for="column in table2.columns" :key="column">{{ column }}</th>
                <th>Ação</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(row, index) in table2.data" :key="index">
                <td v-for="(value, key) in row" :key="key">
                  <!-- Renderizar dropdown somente para a coluna "Estado" -->
                  <template v-if="key === 'estado'">
                    <select @change="updateEstado(index, $event.target.value)" v-model="row.estado">
                      <option value="Confirmado">Confirmado</option>
                      <option value="Pendente">Pendente</option>
                    </select>
                  </template>
                  <!-- Renderizar dropdown somente para a coluna "Guia" -->
                  <template v-else-if="key === 'guia'">
                    <select @change="updateGuia(index, $event.target.value)" v-model="row.guia">
                      <option value="Por Definir">Por Definir</option>
                      <option value="Filipe Almeida">Filipe Almeida</option>
                      <option value="Andre Pereira">Andre Pereira</option>
                      <option value="Matilde Souza">Matilde Souza</option>
                    </select>
                  </template>
                  <!-- Renderizar valor para as outras colunas -->
                  <template v-else>
                    {{ value }}
                  </template>
                </td>
                <td>
                  <button @click="deleteRegistro(index)">Apagar</button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      table2: {
        title: "Table on Plain Background",
        subTitle: "Here is a subtitle for this table",
        columns: [
          "Nome",
          "Telefone",
          "Tour",
          "Numero Participantes",
          "Data",
          "Horas",
          "Preço",
          "Estado",
          "Guia",
        ],
        data: []
      }
    };
  },
  mounted() {
    this.loadTableData();
  },
  methods: {
    loadTableData() {
      const storedRegistros = localStorage.getItem("registros");
      if (storedRegistros) {
        this.table2.data = JSON.parse(storedRegistros);
        this.updateNames();
      } else {
        this.table2.data = [
          {
            nome: "Nome 1",
            telefone: "123456789",
            tour: "Tour A",
            "numero Participantes": 5,
            data: "2023-06-01",
            horas: "10:00",
            preço: 50,
            estado: "Confirmado",
            guia: "Por definir"
          },
          {
            nome: "Nome 2",
            telefone: "987654321",
            tour: "Tour B",
            "numero Participantes": 4,
            data: "2023-06-02",
            horas: "14:00",
            preço: 40,
            estado: "Pendente",
            guia: "Por definir"
          }
        ];

        localStorage.setItem("registros", JSON.stringify(this.table2.data));
      }
    },
    updateEstado(index, value) {
      this.table2.data[index].estado = value;
      localStorage.setItem("registros", JSON.stringify(this.table2.data));
    },
    updateGuia(index, value) {
      this.table2.data[index].guia = value;
      localStorage.setItem("registros", JSON.stringify(this.table2.data));
    },
    deleteRegistro(index) {
      this.table2.data.splice(index, 1);
      localStorage.setItem("registros", JSON.stringify(this.table2.data));
    }
  }
};
</script>

<style></style>
