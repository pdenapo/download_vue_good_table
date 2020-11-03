<template>
<span>
<p>
 <a id="download_latex_link" v-bind:download="file_name" href=”” v-on:click="download_in_latex(columns,rows)">{{label}}</a>
 </p>

</span>
</template>

<script>

export default {
  name: 'DownloadLatex',
  props: ["file_name", "label","columns","rows"],
 methods:
 {
  download_in_latex(columns,rows) {

      // We build a parameter for the longtabu environment with an X for each column, separated with |

      var parameter="|"

       columns.forEach(function (col, col_number) {
           if (col_number >0) parameter += "|"
             parameter += "X"
         })
      parameter+="|"

      // We use the longtabu environment which I believe is the best environment for longtables

      var latex_document ="\\documentclass{article} \n \\usepackage{longtable} \n\\usepackage{tabu} \n\\begin{document} \n \\begin{longtabu}{"+parameter+"} \n \\hline \n"

      // create the header

       columns.forEach(function (col, col_number) {
           if (col_number >0) latex_document += " & "
             latex_document += col.label
         })
         latex_document += "\\\\\n"  
         
      latex_document += "\\hline \n"

      // Now we put the data

      rows.forEach(function (row) {
         columns.forEach(function (col, col_number) {
           if (col_number >0) latex_document += " & "
             latex_document += row[col.field]
         })
         latex_document += "\\\\\n"
      });  
     
     // Now we close the document

      latex_document += "\\hline \n \\end{longtabu} \n \\end{document}\n"

      let latex_mime_type = "application/x-latex;charset=utf-8,header=present";
      var data = new Blob([latex_document], {type: latex_mime_type});
      var url = window.URL.createObjectURL(data);
      document.getElementById('download_latex_link').href = url;  
  }  
  },
};
</script>

<style>
</style>
