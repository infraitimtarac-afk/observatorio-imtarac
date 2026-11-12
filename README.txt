IMTARAC · Observatorio Vial V3
================================

Versión ampliada del sistema de señalización con:

1. Conexión lista para Firebase (Auth + Firestore + Storage)
2. Campo libre cuando eliges "Otro" en Tipo o Elemento de intervención
3. Módulo de HALLAZGOS / inspección de vía:
   - Ancho de calzada
   - Colegio (sí/no) + nombre + hora entrada/salida
   - Defectos: agrietamiento, baches, piel de cocodrilo, endiduras, hundimiento, desgaste, falta de señalización, otro (con texto libre)
   - Severidad
   - Varias fotos por hallazgo
4. Módulo y CAPA de SINIESTROS:
   - Tipo (daños materiales, heridos, daño grave, muerte, choque, atropello, volcamiento, otro)
   - Gravedad, nº lesionados y fallecidos
   - Dirección exacta, fecha/hora, fotos y notas
   - Botón "Solo siniestros" que oculta las otras capas para enfocarse en accidentes
5. Capas independientes (Señalización / Hallazgos / Siniestros) que se pueden mostrar u ocultar
6. Exportación CSV unificada de los tres tipos de registro
7. Importación KML (sigue funcionando para señales)

------------------------------------------------
LOGIN DEMO (modo local)
Usuario: admin
Contraseña: imtarac2026

------------------------------------------------
CÓMO CONECTAR FIREBASE

1. Entra a https://console.firebase.google.com y crea un proyecto.
2. Activa:
   - Authentication → método Email/Password
   - Firestore Database (modo producción o prueba según necesites)
   - Storage
3. En Configuración del proyecto → Tus apps → Web, copia el objeto firebaseConfig.
4. Abre index.html y busca:
      const USE_FIREBASE = false;
   Cámbialo a:
      const USE_FIREBASE = true;
5. Pega tu firebaseConfig (apiKey, authDomain, projectId, etc.).
6. Crea un usuario en Authentication (o usa el demo mientras pruebas).
7. Reglas recomendadas de Firestore (desarrollo):
   allow read, write: if request.auth != null;
8. Reglas de Storage similares.
9. Sube index.html a Netlify, Vercel o GitHub Pages (HTTPS obligatorio para GPS y cámara).

Mientras USE_FIREBASE = false todo se guarda en el navegador (localStorage).
Cuando lo pongas en true, los datos se sincronizan en la nube y las fotos van a Storage.

------------------------------------------------
ESTRUCTURA DE DATOS

Colecciones Firestore (o claves localStorage):
- intervenciones  (señales, demarcación, etc.)
- hallazgos       (estado de vía, colegios, defectos)
- siniestros      (accidentes)

Cada registro lleva lat/lng, dirección, fotos (URL o dataURL) y campos específicos.

------------------------------------------------
PUBLICAR

Solo necesitas subir el archivo index.html.
Para producción con Firebase no hace falta backend propio.
