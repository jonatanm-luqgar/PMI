# JONA OS — sistema operativo personal

Aplicación web responsive, en español, con HTML/CSS/JavaScript modular y Firebase Authentication + Cloud Firestore. Está pensada para publicarse como sitio estático (GitHub Pages o Firebase Hosting). GitHub aloja el código; Firestore sincroniza los datos entre dispositivos.

## Incluye las tres versiones

- **1.0 Fundamentos:** inicio de sesión, áreas de vida, objetivos, proyectos y tareas.
- **2.0 Agile:** Sprints, tablero Kanban, agenda por fechas límite, hábitos y retrospectivas.
- **3.0 Intelligence:** indicadores calculados a partir de los datos y registro manual de ingresos/gastos. Exportación JSON de los datos.

Las tres versiones están en el mismo proyecto y se habilitan con el selector de versión. No hay que migrar datos al pasar de una versión a otra.

## 1. Configurar Firebase

1. En Firebase Console crea un proyecto o reutiliza uno.
2. Añade una aplicación web y copia su configuración.
3. Abre `firebase-config.js` y reemplaza todos los valores `PEGA_AQUI...` / `TU_...` por los valores reales.
4. En **Authentication → Sign-in method**, activa **Correo electrónico/contraseña**.
5. En **Firestore Database**, crea la base de datos.
6. En Firestore → Rules, pega el contenido de `firestore.rules` y publica las reglas.

La estructura de datos será `users/{UID}/{colección}/{documento}`. Cada cuenta solo puede leer y modificar sus propios documentos. No publiques la app con reglas abiertas.

## 2. Ejecutar en local

No abras `index.html` directamente con `file://`, porque los módulos JavaScript necesitan un servidor HTTP. Desde esta carpeta ejecuta, por ejemplo:

```bash
python -m http.server 8000
```

Después abre `http://localhost:8000`.

## 3. Publicar

**GitHub Pages:** sube estos archivos a un repositorio y activa Pages desde Settings → Pages → Deploy from a branch. Firebase Authentication → Settings → Authorized domains debe incluir el dominio de GitHub Pages (por ejemplo `usuario.github.io`).

**Firebase Hosting:** instala Firebase CLI, ejecuta `firebase login`, `firebase init hosting` (directorio público: `.`; configura como SPA: no) y `firebase deploy`. Añade también el dominio de Hosting a los dominios autorizados de Authentication.

## 4. Primer uso

1. Crea una cuenta desde la pantalla de acceso.
2. Crea tus áreas de vida (profesional, económica, salud, intelectual, personal).
3. Define objetivos y vincúlalos a un área.
4. Crea proyectos y tareas.
5. En versión 2.0 planifica Sprints y registra hábitos.
6. En versión 3.0 revisa indicadores y registra movimientos económicos si deseas.

## Notas importantes

- La agenda de esta primera entrega ordena tareas por fecha límite; no es todavía un calendario mensual con bloques horarios.
- Los hábitos guardan registros por fecha; el resumen muestra el total de registros, no una racha inteligente.
- Los indicadores se calculan localmente a partir de tus documentos; no son métricas financieras ni profesionales verificadas.
- La app no contiene una API key de IA. La integración con Gemini puede añadirse más adelante sin exponer claves privadas en el navegador.
- Haz exportaciones JSON periódicas desde **Versión 3.0 → Indicadores**. El archivo descargado es una copia de seguridad manual.
