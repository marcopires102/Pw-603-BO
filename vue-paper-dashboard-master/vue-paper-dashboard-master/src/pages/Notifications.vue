<template>
  <div>
    <div class="col-12">
      <div class="card-plain">
        <div class="table-full-width table-responsive">
          <table class="table">
            <thead>
              <tr>
                <th v-for="column in table3.columns" :key="column">{{ column }}</th>
                <th>Apagar</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(row, index) in table3.data" :key="index">
                <td v-for="(value, key) in row" :key="key">
                  {{ value }}
                </td>
                <td>
                  <button @click="deleteProfile(index)">Apagar</button>
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
      table3: {
        title: "Table on Plain Background",
        subTitle: "Here is a subtitle for this table",
        columns: [
          "Username",
          "Email",
          "Password",
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
      const storedUsers = localStorage.getItem("users");
      if (storedUsers) {
        this.table3.data = JSON.parse(storedUsers);
        this.updateNames();
      } else {
        this.table3.data = [
          {
            username: "user1",
            email: "user1@example.com",
            password: "password1"

          },
          {
            username: "user3",
            email: "user2@example.com",
            password: "password2"

          }
        ];

        localStorage.setItem("users", JSON.stringify(this.table3.data));
      }
    },
    deleteProfile(index) {
      this.table3.data.splice(index, 1);
      localStorage.setItem("users", JSON.stringify(this.table3.data));
    }
  }
};
</script>

<style></style>



