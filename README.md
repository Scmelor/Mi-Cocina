# 🍲 Mi Cocina

App web para planear tus comidas: administra tu **despensa**, explora **recetas colombianas y del mundo en vivo**, y genera un **menú semanal** (almuerzo y cena para 1–2 personas) con la **lista de lo que te falta por mercar**. Incluye **sincronización opcional entre varios dispositivos** en tiempo real.

Es un solo archivo (`index.html`), sin instalación ni servidor propio. Se publica gratis en **GitHub Pages**.

---

## ✨ Qué hace

- **Despensa** · checklist de ingredientes por categorías (🥬 vegetales, 🍎 frutas, 🍖 carnes y pescados, 🫘 granos y legumbres, 🌾 cereales, 🧀 lácteos y huevos, 🧂 condimentos, 🛒 otros). Marca lo que tienes, agrega y elimina.
- **Recetas** · más de 30 recetas colombianas siempre disponibles + **búsqueda en vivo por internet** (italianas, mexicanas, españolas, chinas…) con foto, ingredientes, pasos y video. Cada receta marca en verde lo que **ya tienes** y en rojo lo que **falta**. Desde cualquier receta puedes pulsar **📅 Añadir al menú** para colocarla en el día y la franja que quieras.
- **Crea tus propias recetas** · con **➕ Crear receta** guardas recetas tuyas (nombre, tipo, ingredientes por categoría y pasos). Aparecen en **⭐ Mis recetas**, entran en el menú y en la lista de mercado, y se sincronizan entre dispositivos.
- **Menú semanal, dieta con carne primero** · cada día trae **almuerzo + ensalada + cena**, priorizando **proteína (carne)** y lo que tienes en tu despensa. Incluye **almuerzos balanceados** (proteína + carbohidrato + ensalada), una **categoría de ensalada** con más de 10 opciones (mixta, aguacate y tomate, repollo y zanahoria, César, garbanzos…), y **cenas ligeras y creativas** (arepa o pan con huevo, tacos, quesadillas, wraps, choripán, salchipapa, huevos rancheros…). Con **lista de mercado** agrupada por categoría. Se puede imprimir o guardar como PDF.
- **Menú editable** · **arrastra** una comida para moverla o intercambiarla entre días; **⧉ duplica** una receta a otro día (la misma receta dos días); **🔁 cambia** una comida por otra sugerencia. Los cambios se guardan y se sincronizan.
- **Sincronización multi-dispositivo** (opcional) · con un mismo "código de cocina", tu despensa, menú y lista de mercado se comparten y actualizan **en tiempo real** entre celular, computador, etc.

Las recetas del mundo se traen en vivo de **[TheMealDB](https://www.themealdb.com)** (API pública y gratuita). Lo colombiano funciona incluso sin conexión.

---

## 🚀 Paso 1 · Publicar en GitHub y obtener el link

1. Entra a **https://github.com** e inicia sesión (crea una cuenta gratis si no tienes).
2. Arriba a la derecha pulsa **+ → New repository**.
3. Nombre del repo: por ejemplo `mi-cocina`. Déjalo **Public** y crea el repositorio.
4. Pulsa **Add file → Upload files**, sube **`index.html`** (y este `README.md` si quieres) y pulsa **Commit changes**.
5. Ve a **Settings → Pages** (menú lateral).
6. En **Build and deployment → Source** elige **Deploy from a branch**, rama **`main`**, carpeta **`/root`**, y pulsa **Save**.
7. Espera ~1 minuto y recarga. Aparecerá tu link:

   ```
   https://TU-USUARIO.github.io/mi-cocina/
   ```

Ese es el enlace de tu app. Ábrelo en el celular y el computador y guárdalo en favoritos. Cada vez que actualices `index.html`, la página se actualiza sola.

> 💡 También puedes abrir `index.html` con doble clic en tu computador para usarla sin publicarla (en modo local).

---

## 🔄 Paso 2 · Activar la sincronización entre dispositivos (opcional pero recomendado)

Para que **varios dispositivos actualicen al mismo tiempo**, la app usa **Firebase Realtime Database** de Google (plan gratuito). Se configura una sola vez.

### A. Crear el proyecto y la base de datos

1. Entra a **https://console.firebase.google.com** con tu cuenta de Google.
2. **Add project / Agregar proyecto** → ponle un nombre (ej. `mi-cocina`) → puedes **desactivar Google Analytics** → **Crear**.
3. En el menú lateral abre **Build → Realtime Database** → **Create Database**.
4. Elige la ubicación (ej. *United States*) → en las reglas de seguridad elige **Start in test mode** (modo de prueba) → **Enable**.
5. En **Project Overview** (⚙️ arriba a la izquierda) → **Project settings** → baja hasta **Your apps** → pulsa el ícono **`</>` (Web)**.
6. Registra la app (un apodo cualquiera, sin hosting) → Firebase te mostrará un bloque **`firebaseConfig`** parecido a este:

   ```js
   const firebaseConfig = {
     apiKey: "AIza…",
     authDomain: "mi-cocina.firebaseapp.com",
     databaseURL: "https://mi-cocina-default-rtdb.firebaseio.com",
     projectId: "mi-cocina",
     storageBucket: "mi-cocina.appspot.com",
     messagingSenderId: "1234567890",
     appId: "1:1234567890:web:abcdef"
   };
   ```

   > ⚠️ Debe incluir **`databaseURL`**. Si no aparece, es porque falta el paso 3–4 (crear la Realtime Database).

### B. Conectar la app

1. Abre tu app (el link de GitHub Pages) y pulsa el ícono **⚙️** arriba a la derecha.
2. En **Código de tu cocina** escribe algo fácil de recordar, ej. `cocina-silvia`. **Usa el mismo código en todos los dispositivos.**
3. En **Configuración de Firebase** pega el bloque `firebaseConfig` completo (con las llaves `{ }`).
4. Pulsa **Conectar**. El indicador de arriba pasará a **“Sincronizado”**.
5. Repite en tu otro dispositivo con el **mismo código** y la **misma configuración**. Listo: lo que marques en uno aparece en el otro al instante.

### Nota de seguridad

El “modo de prueba” de Firebase deja la base abierta por ~30 días. Para uso doméstico y privado es suficiente. Si quieres restringir el acceso, en **Realtime Database → Rules** puedes limitar por un código secreto o activar autenticación. Como el código va en un sitio público, no guardes datos sensibles.

---

## 🔧 Personalizar

- **Agregar recetas colombianas:** en `index.html` busca `const COL = [...]` y copia el formato de una receta (nombre, `tipo` `almuerzo`/`cena`, ingredientes `[nombre, cantidad, categoría]` y `pasos`).
- **Despensa inicial:** edita `PANTRY_DEFAULTS`.
- Las recetas colombianas están pensadas para **2 personas**.

---

Hecho con ♥ para cocinar rico. Recetas del mundo vía TheMealDB · Sincronización con Firebase.
