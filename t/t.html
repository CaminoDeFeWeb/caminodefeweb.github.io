<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <title>Mendoza Transit - API Real (Fix)</title>
  
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" />
  
  <style>
    :root { --primary: #2e7d32; --tram: #d32f2f; }
    body, html { margin: 0; padding: 0; height: 100%; font-family: 'Segoe UI', sans-serif; overflow: hidden; }
    #map { height: 100vh; width: 100%; z-index: 1; }
    .top-bar {
      position: absolute; top: 15px; left: 15px; right: 15px;
      background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(10px);
      padding: 15px; border-radius: 12px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.2); z-index: 1000;
    }
    .top-bar h1 { margin: 0 0 10px 0; font-size: 1.2rem; color: #333; }
    .status { font-size: 0.85rem; font-weight: bold; display: flex; align-items: center; gap: 5px; }
    .fab-location {
      position: absolute; bottom: 30px; right: 20px; z-index: 1000;
      width: 50px; height: 50px; background: white; border-radius: 50%;
      display: flex; justify-content: center; align-items: center;
      box-shadow: 0 4px 15px rgba(0,0,0,0.2); cursor: pointer; border: none;
      font-size: 1.2rem; color: #333;
    }
    .custom-icon {
      background: white; border-radius: 50%; border: 2px solid;
      display: flex; justify-content: center; align-items: center;
      box-shadow: 0 3px 6px rgba(0,0,0,0.3); font-size: 1.1rem; color: white;
    }
    .icon-bike { background-color: var(--primary); border-color: white; }
    .icon-tram { background-color: var(--tram); border-color: white; }
    .popup-title { font-weight: bold; border-bottom: 1px solid #ccc; padding-bottom: 5px; margin-bottom: 5px; }
  </style>
</head>
<body>

  <div class="top-bar">
    <h1>Mendoza OpenData <i class="fa-solid fa-server"></i></h1>
    <div class="status" id="api-status" style="color: #1976d2;">
      <i class="fa-solid fa-spinner fa-spin"></i> Conectando...
    </div>
  </div>

  <button class="fab-location" onclick="locateUser()">
    <i class="fa-solid fa-location-crosshairs"></i>
  </button>

  <div id="map"></div>

  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

  <script>
    // 1. Inicializar Mapa (Centrado en el Gran Mendoza / Maipú)
    const map = L.map('map', { zoomControl: false }).setView([-32.930, -68.820], 12);
    L.tileLayer('https://{s}.basemaps.cartocdn.com/rastertiles/voyager/{z}/{x}/{y}{r}.png', {
      maxZoom: 19, attribution: '&copy; OpenStreetMap'
    }).addTo(map);
    L.control.zoom({ position: 'bottomleft' }).addTo(map);

    const layers = {
      bike: L.layerGroup().addTo(map),
      tram: L.layerGroup().addTo(map)
    };

    const bikeIcon = L.divIcon({ html: `<div class="custom-icon icon-bike"><i class="fa-solid fa-bicycle"></i></div>`, className: '', iconSize: [30, 30] });
    const tramIcon = L.divIcon({ html: `<div class="custom-icon icon-tram"><i class="fa-solid fa-train-tram"></i></div>`, className: '', iconSize: [30, 30] });

    // 2. CONEXIÓN A API REAL CON MÉTODO POST (Más seguro)
    async function fetchRealMendozaData() {
      const statusEl = document.getElementById('api-status');
      
      const query = `
        [out:json][timeout:25];
        (
          node["amenity"="bicycle_rental"](-33.05,-68.95,-32.80,-68.70);
          node["railway"="tram_stop"](-33.05,-68.95,-32.80,-68.70);
        );
        out body;
      `;

      try {
        // Usamos POST en lugar de GET para evitar que el navegador rompa la URL
        const response = await fetch('https://overpass-api.de/api/interpreter', {
          method: 'POST',
          body: "data=" + encodeURIComponent(query),
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded'
          }
        });

        if (!response.ok) {
          throw new Error(`Error del servidor: ${response.status}`);
        }

        const data = await response.json();

        let bikeCount = 0;
        let tramCount = 0;

        data.elements.forEach(element => {
          const lat = element.lat;
          const lon = element.lon;
          const tags = element.tags || {};
          const name = tags.name || "Punto sin nombre";

          if (tags.amenity === "bicycle_rental") {
            const marker = L.marker([lat, lon], { icon: bikeIcon });
            marker.bindPopup(`<div class="popup-title">🚲 ${name}</div>`);
            layers.bike.addLayer(marker);
            bikeCount++;
          } else if (tags.railway === "tram_stop") {
            const marker = L.marker([lat, lon], { icon: tramIcon });
            marker.bindPopup(`<div class="popup-title">🚋 ${name}</div>`);
            layers.tram.addLayer(marker);
            tramCount++;
          }
        });

        if (bikeCount === 0 && tramCount === 0) {
          statusEl.innerHTML = `<i class="fa-solid fa-circle-exclamation" style="color: orange;"></i> Conectado, pero no se hallaron datos.`;
        } else {
          statusEl.innerHTML = `<i class="fa-solid fa-check" style="color: green;"></i> Reales: ${bikeCount} bicis, ${tramCount} tranvías.`;
          statusEl.style.color = "green";
        }

      } catch (error) {
        // Mostrará el error exacto en rojo
        statusEl.innerHTML = `<i class="fa-solid fa-triangle-exclamation"></i> Error: ${error.message}`;
        statusEl.style.color = "red";
        console.error(error);
      }
    }

    // 3. GEOLOCALIZACIÓN
    function locateUser() {
      map.locate({ setView: true, maxZoom: 16 });
    }

    map.on('locationfound', function(e) {
      L.circleMarker(e.latlng, { radius: 8, fillColor: "#1976d2", color: "#fff", weight: 3, fillOpacity: 1 })
       .addTo(map).bindPopup("Tu ubicación").openPopup();
    });

    fetchRealMendozaData();
  </script>
</body>
</html>
