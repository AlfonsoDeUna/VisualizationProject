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

[back](./)
