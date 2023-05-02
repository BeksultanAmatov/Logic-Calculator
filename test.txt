function generateTable() {
  var variables = document.getElementById("variables").value.replace(/\s/g, "").split(",");
  var expression = document.getElementById("expression").value.replace(/\s/g, "");

  // Generate table headers
  var tableHeaders = "<th>" + variables.join("</th><th>") + "</th><th>" + expression + "</th><tr>";

  // Generate table rows
  var tableRows = "";
  for (var i = 0; i < Math.pow(2, variables.length); i++) {
      var binary = i.toString(2);
      while (binary.length < variables.length) {
          binary = "0" + binary;
      }
      var row = "<td>" + binary.split("").join("</td><td>") + "</td><td>" + eval(expression.replace(/([a-z])/g, "binary.charAt(variables.indexOf('$1'))")) + "</td><tr>";
      tableRows += row;
  }

  // Generate table
  var table = "<table><thead><tr>" + tableHeaders + "</tr></thead><tbody>" + tableRows + "</tbody></table>";
  document.getElementById("tableContainer").innerHTML = table;
}


var divIds = ["div1", "div2", "div3", "div4"];
var currentDivIndex = 0;

function showDiv(index) {
  var divs = document.getElementsByTagName("div");
  
  for (var i = 0; i < divs.length; i++) {
    if (divIds.indexOf(divs[i].id) !== -1) {
      divs[i].style.display = "none";
    }
  }
  
  var divToShow = document.getElementById(divIds[index]);
  divToShow.style.display = "block";
  currentDivIndex = index;
}

function showNext() {
  if (currentDivIndex < divIds.length - 1) {
    showDiv(currentDivIndex + 1);
  }
}

function showPrev() {
  if (currentDivIndex > 0) {
    showDiv(currentDivIndex - 1);
  }
}

showDiv(currentDivIndex);
