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
                <td v-for="(value, key) in row" :key="key">{{ value }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>





<script>



import { PaperTable } from "@/components";

export default {
  components: {
    PaperTable,
  },
  data() {
    return {
      table2: {
        title: "Table on Plain Background",
        subTitle: "Here is a subtitle for this table",
        columns: ["Username", "Nome", "Telefone", "Tour", "Numero Participantes","Data","Horas","Preço","Estado"],
        data: [],
      },
    };
  },
  mounted() {
    // Retrieve "reservas" data from local storage
    const storedRegistros = localStorage.getItem("registros");
    if (storedRegistros) {
      this.table2.data = JSON.parse(storedRegistros);
    }
  },
};
</script>
<style></style>
