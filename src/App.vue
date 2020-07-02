<template>
<span>
  <div>
    <vue-good-table
      :columns="columns"
      :rows="rows"
      theme="black-rhino" />
  </div>

<br> 

  <DownloadCsv v-bind:columns="columns" v-bind:rows="rows" label="Download in CSV format." file_name="table.cvs" />

</span>
</template>

<script>
import DownloadCsv from "@/DownloadCsv";
import 'vue-good-table/dist/vue-good-table.css'
import { VueGoodTable } from "vue-good-table";

export default {
  name: 'App',
  components: {
  VueGoodTable,
  DownloadCsv
 },
  data(){
    return {
      // Example data from Vue.js tutorial 
      // https://xaksis.github.io/vue-good-table/guide/#basic-example
      columns: [
        {
          label: 'Name',
          field: 'name',
        },
        {
          label: 'Age',
          field: 'age',
          type: 'number',
        },
        {
          label: 'Created On',
          field: 'createdAt',
          type: 'date',
          dateInputFormat: 'yyyy-MM-dd',
          dateOutputFormat: 'MMM Do yy',
        },
        {
          label: 'Percent',
          field: 'score',
          type: 'percentage',
        },
      ],
      rows: [
        { id:1, name:"John", age: 20, createdAt: '2012-01-01',score: 0.03343 },
        { id:2, name:"Jane", age: 24, createdAt: '2011-10-31', score: 0.03343 },
        { id:3, name:"Susan", age: 16, createdAt: '2011-10-30', score: 0.03343 },
        { id:4, name:"Chris", age: 55, createdAt: '2011-10-11', score: 0.03343 },
        { id:5, name:"Dan", age: 40, createdAt: '2011-10-21', score: 0.03343 },
        { id:6, name:"John", age: 20, createdAt: '2011-10-31', score: 0.03343 },
      ],
    };
  },
};
</script>

<style scoped>
span { 
padding-left: 80px;
}
</style>
