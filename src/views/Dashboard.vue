<template>
  <div>
    <h1>Dashboard</h1>
    <v-spacer></v-spacer>
    <v-data-table
      :headers="headers"
      :items="employees"
      :multi-sort = 'true'
      class="elevation-1"
      @click:row="selectRow"
    ></v-data-table>
    <v-snackbar v-model="snackbar">
      You have selected {{ selectedEmployee.name }},
      {{ selectedEmployee.title}}

      <template v-slot:action="{ attrs }">
        <v-btn color="pink" text v-bind="attrs" @click="snackbar = false">
          Close
        </v-btn>
      </template>
    </v-snackbar>
  </div>
</template>

<script>
import employeesData from '../assets/test.json'
export default {
  data() {
    return {
      selectedEmployee: {
        name:'',
        title:''
      },
      snackbar: false,
      headers: [
        {
          text: "Name",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "Title", value: "title" },
      ],
      employees: employeesData.employees,
    };
  },
  methods: {
    selectRow(event) {
      this.snackbar = true;
      this.selectedEmployee.name = event.name;
      this.selectedEmployee.title = event.title;
    },
  },
};
</script>
<style>
</style>