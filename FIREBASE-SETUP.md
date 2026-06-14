# Sincronización entre dispositivos (Firebase) — setup de ~5 min

La app funciona sin esto (cada equipo guarda su propia data). Esto sirve para que **las notas y la evaluación del viernes se compartan en vivo** entre todos los celulares.

Lo haces **una sola vez** (crear el proyecto). Es gratis; el uso de una familia está MUY por debajo del tier gratis de Firebase.

## 1. Crear el proyecto
1. Entra a https://console.firebase.google.com con tu cuenta Google.
2. **Crear un proyecto** → nombre `banco-de-tiempo` → puedes **desactivar** Google Analytics → Crear.

## 2. Crear la base de datos
1. Menú izquierdo: **Compilación → Firestore Database** → **Crear base de datos**.
2. Modo **producción** → ubicación `southamerica-east1` (o `nam5`) → **Habilitar**.
3. Pestaña **Reglas (Rules)** → reemplaza todo por esto y **Publicar**:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /families/{code} {
      allow read, write: if request.auth != null;
    }
  }
}
```

## 3. Habilitar login anónimo
1. **Compilación → Authentication** → **Comenzar**.
2. Pestaña **Sign-in method** → habilita **Anónimo (Anonymous)** → Guardar.

## 4. Registrar la app web y copiar la config
1. Engranaje ⚙️ (arriba izq.) → **Configuración del proyecto**.
2. Baja a **Tus apps** → ícono web **`</>`** → registra (apodo: `web`) → **NO** marques Hosting.
3. Te muestra un bloque `const firebaseConfig = { ... };`. **Copia desde `{` hasta `}`** (puedes copiar el bloque entero, la app lo entiende).

## 5. Conectar cada celular
En **cada** dispositivo (tu celular, el de Lucía, el de Joaquín, tablet…):
1. Abre la app → **Ajustes** (PIN) → **☁️ Sincronización entre dispositivos**.
2. **Código de familia**: invéntalo difícil (ej. `salmon-4f9c2ax7`) y usa **EL MISMO en todos los equipos**. Es el secreto que une a la familia — no lo compartas fuera.
3. **Config de Firebase**: pega el bloque del paso 4.
4. **Guardar y conectar** → debe decir **✓ Conectado**.

Listo. A partir de ahí, lo que evalúes el viernes aparece en los demás celulares en segundos.

## Notas
- El **código de familia** es la seguridad: cualquiera que lo sepa (y tenga la config pública) puede leer/escribir la data de tu familia. Por eso hazlo largo y no lo publiques.
- La config de Firebase (`apiKey`, etc.) **no es secreta** — es seguro que esté en el navegador; la protección real son las Reglas + el código de familia.
- Si algún día quieres apagarlo: Ajustes → **Desconectar**.
