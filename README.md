<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Recomendador de Perfumes</title>

<!-- Google AdSense (pon aquí tu código de editor) -->
<script data-ad-client="ca-pub-XXXXXXXXXXXXXX" async
  src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>

<style>
  body {
    font-family: Arial, sans-serif;
    background: #fafafa;
    margin: 20px;
  }
  h1, h2 {
    text-align: center;
  }
  form {
    max-width: 400px;
    margin: auto;
    background: white;
    padding: 20px;
    border-radius: 8px;
  }
  label {
    display: block;
    margin-top: 15px;
  }
  select, button {
    width: 100%;
    padding: 8px;
    margin-top: 5px;
  }
  #result {
    max-width: 400px;
    margin: 20px auto;
    background: white;
    padding: 15px;
    border-radius: 8px;
    text-align: center;
  }
  .ad-container {
    max-width: 400px;
    margin: 20px auto;
    text-align: center;
  }
</style>
</head>
<body>

<h1>Encuentra tu perfume ideal</h1>

<!-- Anuncio superior -->
<div class="ad-container">
  <ins class="adsbygoogle"
       style="display:block"
       data-ad-client="ca-pub-XXXXXXXXXXXXXX"
       data-ad-slot="1111111111"
       data-ad-format="auto"
       data-full-width-responsive="true"></ins>
</div>

<form id="perfumeForm">
  <label for="aroma">¿Prefieres aromas dulces o frescos?</label>
  <select id="aroma" name="aroma" required>
    <option value="">Selecciona...</option>
    <option value="dulce">Dulce</option>
    <option value="fresco">Fresco</option>
  </select>

  <label for="momento">¿Para qué momento?</label>
  <select id="momento" name="momento" required>
    <option value="">Selecciona...</option>
    <option value="día">Día</option>
    <option value="noche">Noche</option>
  </select>

  <label for="precio">¿Cuál es tu presupuesto?</label>
  <select id="precio" name="precio" required>
    <option value="">Selecciona...</option>
    <option value="bajo">Menos de 50€</option>
    <option value="medio">50€ - 100€</option>
    <option value="alto">Más de 100€</option>
  </select>

  <button type="submit" style="margin-top: 20px;">Obtener recomendación</button>
</form>

<div id="result"></div>

<!-- Anuncio inferior -->
<div class="ad-container">
  <ins class="adsbygoogle"
       style="display:block"
       data-ad-client="ca-pub-XXXXXXXXXXXXXX"
       data-ad-slot="2222222222"
       data-ad-format="auto"
       data-full-width-responsive="true"></ins>
</div>

<script>
  const form = document.getElementById('perfumeForm');
  const resultDiv = document.getElementById('result');

  form.addEventListener('submit', function(e) {
    e.preventDefault();

    const aroma = form.aroma.value;
    const momento = form.momento.value;
    const precio = form.precio.value;

    let perfume;

    if (aroma === 'dulce' && momento === 'noche') {
      if (precio === 'alto') perfume = 'Yves Saint Laurent Black Opium';
      else if (precio === 'medio') perfume = 'La Vie Est Belle de Lancôme';
      else perfume = 'Ariana Grande Cloud';
    } else if (aroma === 'fresco' && momento === 'día') {
      if (precio === 'alto') perfume = 'Chanel Chance Eau Fraîche';
      else if (precio === 'medio') perfume = 'Light Blue de Dolce & Gabbana';
      else perfume = 'Elizabeth Arden Green Tea';
    } else {
      perfume = 'Versace Bright Crystal';
    }

    if (!navigator.geolocation) {
      resultDiv.innerHTML = `<h2>Recomendación: ${perfume}</h2><p>Tu navegador no soporta geolocalización para mostrar tiendas cercanas.</p>`;
      return;
    }

    navigator.geolocation.getCurrentPosition(
      (pos) => {
        const lat = pos.coords.latitude;
        const lon = pos.coords.longitude;
        const mapsUrl = `https://www.google.com/maps/search/perfumerías/@${lat},${lon},14z`;

        resultDiv.innerHTML = `
          <h2>Recomendación: ${perfume}</h2>
          <p><a href="${mapsUrl}" target="_blank">Ver tiendas cerca de ti en Google Maps</a></p>
        `;
      },
      (err) => {
        resultDiv.innerHTML = `
          <h2>Recomendación: ${perfume}</h2>
          <p>Activa la ubicación para ver tiendas cerca de ti.</p>
        `;
      }
    );
  });
</script>

</body>
</html>
