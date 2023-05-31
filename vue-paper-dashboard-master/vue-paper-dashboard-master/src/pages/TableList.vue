<template>
  <div>
    <div class="col-12">
      <div class="card-plain">
        <div class="table-full-width table-responsive">
          <table class="table">
            <thead>
              <tr>
                <th v-for="column in table2.columns" :key="column">{{ column }}</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(row, index) in table2.data" :key="index">
                <td v-for="(value, key) in row" :key="key">
                  <!-- Renderizar dropdown somente para a coluna "Estado" -->
                  <template v-if="key === 'Estado'">
                    <select @change="updateEstado(index, $event.target.value)" v-model="row.Estado">
                      <option value="Confirmado">Confirmado</option>
                      <option value="Pendente">Pendente</option>
                    </select>
                  </template>
                  <!-- Renderizar valor para as outras colunas -->
                  <template v-else>
                    {{ value }}
                  </template>
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
          "Username",
          "Nome",
          "Telefone",
          "Tour",
          "Numero Participantes",
          "Data",
          "Horas",
          "Preço",
          "Estado"
        ],
        data: []
      }
    };
  },
  mounted() {
    // Retrieve "registros" data from local storage
    const storedRegistros = localStorage.getItem("registros");
    if (storedRegistros) {
      this.table2.data = JSON.parse(storedRegistros);
    } else {
      // Fallback data if no data in local storage
      this.table2.data = [
        {
          Username: "user1",
          Nome: "Nome 1",
          Telefone: "123456789",
          Tour: "Tour A",
          "Numero Participantes": 5,
          Data: "2023-06-01",
          Horas: "10:00",
          Preço: 50,
          Estado: "Confirmado"
        },
        {
          Username: "user2",
          Nome: "Nome 2",
          Telefone: "987654321",
          Tour: "Tour B",
          "Numero Participantes": 3,
          Data: "2023-06-02",
          Horas: "14:00",
          Preço: 40,
          Estado: "Pendente"
        }
        // Add more data objects as needed
      ];

      // Save data to local storage
      localStorage.setItem("registros", JSON.stringify(this.table2.data));
    }
  },
  methods: {
    updateEstado(index, value) {
      // Atualizar o valor "Estado" do item selecionado e salvar no Local Storage
      this.table2.data[index].Estado = value;
      localStorage.setItem("registros", JSON.stringify(this.table2.data));
    }
  }
};
</script>

<style></style>
