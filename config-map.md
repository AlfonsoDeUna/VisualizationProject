## Crear un heatmap en GoogleMaps


### Creación del mapa y las librerías

```
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8">
<link type="text/css" href="css/estilo.css" rel="stylesheet" media="all" />
<script type="text/javascript"
src="http://maps.google.com/maps/api/js?key=aqui-miclave&sensor=false"></script>
<title>GoogleMaps APIv3</title>
</head>
<body>
<div id="mapa"></div>
</body>
</html>
```

> Para ver el mapa al completo

Añadir el siguiente CSS (fichero CSS o con Style)

```
#mapa {
width: 100%;
height: 500px;
border: 1px solid #000;
}
```


### Carga de la librería de visualización

```
<script type="text/javascript"
  src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY&libraries=visualization">
</script>

```

### Añadir los puntos en el mapa con su frecuencia

/* Data points defined as a mixture of WeightedLocation and LatLng objects */
var heatMapData = [
  {location: new google.maps.LatLng(37.782, -122.447), weight: 0.5},
  new google.maps.LatLng(37.782, -122.445),
  {location: new google.maps.LatLng(37.782, -122.443), weight: 2},
  {location: new google.maps.LatLng(37.782, -122.441), weight: 3},
  {location: new google.maps.LatLng(37.782, -122.439), weight: 2},
  new google.maps.LatLng(37.782, -122.437),
  {location: new google.maps.LatLng(37.782, -122.435), weight: 0.5},

  {location: new google.maps.LatLng(37.785, -122.447), weight: 3},
  {location: new google.maps.LatLng(37.785, -122.445), weight: 2},
  new google.maps.LatLng(37.785, -122.443),
  {location: new google.maps.LatLng(37.785, -122.441), weight: 0.5},
  new google.maps.LatLng(37.785, -122.439),
  {location: new google.maps.LatLng(37.785, -122.437), weight: 2},
  {location: new google.maps.LatLng(37.785, -122.435), weight: 3}
];

### Las coordenadas geográficas de Madrid son:

Longitud: -3.7025600
Latitud: 40.4165000

```

### Por último código para visualización 
```
var madrid = new google.maps.LatLng(40.4165000, -3.7025600);
map = new google.maps.Map(document.getElementById('map'), {
  center: madrid,
  zoom: 13,
  mapTypeId: 'satellite'
});

var heatmap = new google.maps.visualization.HeatmapLayer({
  data: heatMapData
});
heatmap.setMap(map);

´´´
