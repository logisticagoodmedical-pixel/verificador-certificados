# verificador-certificados
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Verificador de Certificados</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h1>Verificador de Certificados</h1>
    <input type="text" id="codigo" placeholder="Ingresa tu código de certificado">
    <button onclick="verificar()">Verificar</button>
    <div id="resultado"></div>
  </div>

  <script>
    async function verificar() {
      const codigo = document.getElementById("codigo").value.trim().toUpperCase();
      const resultado = document.getElementById("resultado");
      resultado.innerHTML = "🔎 Buscando...";
      try {
        const response = await fetch("certificados.json");
        const data = await response.json();
        const certificado = data.find(c => c.codigo === codigo);
        if (certificado) {
          resultado.innerHTML = `
            ✅ <strong>Código válido</strong><br>
            <b>Nombre:</b> ${certificado.nombre}<br>
            <b>Curso:</b> ${certificado.curso}<br>
            <b>Fecha:</b> ${certificado.fecha}<br>
            <a href="${certificado.link}" target="_blank">📄 Ver certificado</a>
          `;
        } else {
          resultado.innerHTML = "❌ Código inválido. Verifica e intenta nuevamente.";
        }
      } catch (error) {
        resultado.innerHTML = "❌ Error al cargar los datos.";
      }
    }
  </script>
</body>
</html>
