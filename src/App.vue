<template>
<span>
  <div>
    <vue-good-table
      :columns="columns"
      :rows="rows"
      theme="black-rhino" />
  </div>

<br> 
<p>
 <a id="download_csv_link" download="archivo.csv" href=”” v-on:click="download_in_csv(columns,rows)">Download in CSV Format</a>
 </p>
</span>

</template>

<script>
import 'vue-good-table/dist/vue-good-table.css'
import { VueGoodTable } from "vue-good-table";

export default {
  name: 'App',
  components: {
  VueGoodTable,
 },
 methods:
 {
  download_in_csv(columns,rows) {

// https://stackoverflow.com/questions/14964035/how-to-export-javascript-array-info-to-csv-on-client-side
      
      var csv_spreadsheet =""

      // create the header

       columns.forEach(function (col, col_number) {
           if (col_number >0) csv_spreadsheet += ","
             csv_spreadsheet += col.label
         })
         csv_spreadsheet += "\n"   

      rows.forEach(function (row) {
         columns.forEach(function (col, col_number) {
           if (col_number >0) csv_spreadsheet += ","
             csv_spreadsheet += row[col.field]
         })
         csv_spreadsheet += "\n"
      });  
     
      let csv_mime_type = "text/csv;charset=utf-8,header=present";
      var data = new Blob([csv_spreadsheet], {type: csv_mime_type});
      var url = window.URL.createObjectURL(data);
      document.getElementById('download_csv_link').href = url;  
  }  
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

<style>
</style>
