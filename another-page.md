---
layout: default
---

## Obtención de los datos

En esta primera parte, es importante obtener los datos.


### Página para obtener los datos (PORTAL DE DATOS ABIERTOS DEL AYUNTAMIENTO DE MADRID)

https://datos.madrid.es/portal/site/egob/menuitem.c05c1f754a33a9fbe4b2e4b284f1a5a0/?vgnextoid=fa677996afc6f510VgnVCM1000001d4a900aRCRD&vgnextchannel=374512b9ace9f310VgnVCM100000171f5a0aRCRD&vgnextfmt=default

### Código para subir el fichero a un Google Sheet

```
function importCSVFromWeb() {

  // Provide the full URL of the CSV file.
  var csvUrl = "https://ctrlq.org/data.csv";
  var csvContent = UrlFetchApp.fetch(csvUrl).getContentText();
  var csvData = Utilities.parseCsv(csvContent);

  var sheet = SpreadsheetApp.getActiveSheet();
  sheet.getRange(1, 1, csvData.length, csvData[0].length).setValues(csvData);

}
```
### Código para subir a Google Sheet un CSV pero teniendo en cuenta el separador


Expresiones regulares: https://github.com/google/re2/wiki/Syntax

```
function myFunction() {
  importData();
}

function importData() {
    var ss = SpreadsheetApp.getActive();
    var url = 'https://datos.madrid.es/egob/catalogo/300177-4-bomberos-actuaciones.csv';
    var file = UrlFetchApp.fetch(url); // get feed
 
 
    var csv = file.getBlob().getDataAsString();
    var csvData = CSVToArray(csv,';'); // see below for CSVToArray function
    var sheet = ss.getActiveSheet();
    for (var i = 0, lenCsv = csvData.length; i < lenCsv; i++) {
        sheet.getRange(i + 1, 1, 1, csvData[i].length).setValues(new Array(csvData[i]));
    }
 
};
 
 
// http://www.bennadel.com/blog/1504-Ask-Ben-Parsing-CSV-Strings-With-Javascript-Exec-Regular-Expression-Command.htm
// This will parse a delimited string into an array of
// arrays. The default delimiter is the comma, but this
// can be overriden in the second argument.
 
function CSVToArray(strData, strDelimiter) {
    // Check to see if the delimiter is defined. If not,
    // then default to COMMA.
    strDelimiter = (strDelimiter || ",");
 
    // Create a regular expression to parse the CSV values.
    var objPattern = new RegExp(
        (
            // Delimiters.
            "(\\" + strDelimiter + "|\\r?\\n|\\r|^)" +
 
            // Quoted fields.
            "(?:\"([^\"]*(?:\"\"[^\"]*)*)\"|" +
 
            // Standard fields.
            "([^\"\\" + strDelimiter + "\\r\\n]*))"
        ),
        "gi"
    );
 
    // Create an array to hold our data. Give the array
    // a default empty first row.
    var arrData = [
        []
    ];
 
    // Create an array to hold our individual pattern
    // matching groups.
    var arrMatches = null;
 
    // Keep looping over the regular expression matches
    // until we can no longer find a match.
    while (arrMatches = objPattern.exec(strData)) {
 
        // Get the delimiter that was found.
        var strMatchedDelimiter = arrMatches[1];
 
        // Check to see if the given delimiter has a length
        // (is not the start of string) and if it matches
        // field delimiter. If id does not, then we know
        // that this delimiter is a row delimiter.
        if (
            strMatchedDelimiter.length &&
            (strMatchedDelimiter != strDelimiter)
        ) {
 
            // Since we have reached a new row of data,
            // add an empty row to our data array.
            arrData.push([]);
 
        }
 
        // Now that we have our delimiter out of the way,
        // let's check to see which kind of value we
        // captured (quoted or unquoted).
        if (arrMatches[2]) {
 
            // We found a quoted value. When we capture
            // this value, unescape any double quotes.
            var strMatchedValue = arrMatches[2].replace(
                new RegExp("\"\"", "g"),
                "\""
            );
 
        } else {
 
            // We found a non-quoted value.
            var strMatchedValue = arrMatches[3];
 
        }
 
        // Now that we have our value string, let's add
        // it to the data array.
        arrData[arrData.length - 1].push(strMatchedValue);
    }
 
    // Return the parsed data.
    return (arrData);
};
```

[back](./)
