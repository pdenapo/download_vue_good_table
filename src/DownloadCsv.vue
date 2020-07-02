<template>
<span>
<p>
 <a id="download_csv_link" v-bind:download="file_name" href=”” v-on:click="download_in_csv(columns,rows)">{{label}}</a>
 </p>

</span>
</template>

<script>

export default {
  name: 'DownloadCsv',
  props: ["file_name", "label","columns","rows"],
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
};
</script>

<style>
</style>
