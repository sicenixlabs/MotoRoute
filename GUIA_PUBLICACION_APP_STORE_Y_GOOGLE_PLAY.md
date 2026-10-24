# 🏍️ Guía de Producción Móvil: Cómo Publicar y Bajar MotoRuta desde el App Store (iPhone) y Google Play (Android)

## 1. ¿Por qué MotoRuta usa arquitectura nativa Capacitor 6 sobre Supabase Cloud?
En una moto, un navegador web común (Safari o Chrome) **corta el GPS a los 30 segundos de bloquear la pantalla** o al guardar el teléfono en el bolsillo de la campera.
Con este proyecto nativo **Capacitor 6 (`ar.com.motoruta.app`)**:
- **GPS en Segundo Plano Real (`UIBackgroundModes: location` en iOS y `FOREGROUND_SERVICE_LOCATION` en Android):** Tu posición sigue actualizándose en vivo en el radar de **1° Rodadas en Conjunto (*Pack Ride*)** aunque apagues la pantalla para ahorrar batería o uses Waze encima.
- **Notificaciones Push Nativas (APNs + Firebase FCM):** Cuando un compañero de **`👥 Mi Grupo`** toca *"🚀 Lanzar Rodada"*, a todo el equipo le suena la alerta en el celular aunque tengan la app cerrada.
- **Pantalla Siempre Encendida en Soporte de Manillar (`KeepAwake` / `WakeLock`):** Evita que el tablero se apague mientras vas rodando con guantes.

---

## 2. Ruta A: Cómo subirla y bajarla en el **App Store de Apple (iPhone / iOS)**
1. **Crear cuenta Apple Developer ($99 USD / año):**
   - Ingresá en [developer.apple.com](https://developer.apple.com) y activá tu membresía.
   - En *Certificates, Identifiers & Profiles*, registrá el **Bundle ID** `ar.com.motoruta.app` marcando **Push Notifications** y **Background Modes**.
2. **Compilar sin necesitar una Mac física (usando GitHub Actions incluido):**
   - Subí el contenido de este ZIP a un repositorio privado en tu cuenta de GitHub.
   - El archivo `.github/workflows/build_mobile_stores.yml` alquila automáticamente un servidor `macos-14` con Xcode en la nube de GitHub y genera el paquete de iOS.
   - Si tenés una Mac, simplemente abrí la terminal en esta carpeta y ejecutá:
     ```bash
     npm install
     npx cap sync ios
     npx cap open ios
     ```
3. **Instalar hoy mismo en tu iPhone y el de tu grupo con TestFlight (sin esperar la revisión final):**
   - En Xcode (o vía GitHub Actions), subí el build a **App Store Connect**.
   - Entrá a la pestaña **TestFlight**, agregá los correos de tus amigos de *La Barra de los Domingos* y todos reciben un link oficial de Apple para bajar **MotoRuta** directo en sus iPhones.
4. **Aprobación pública en el App Store:**
   - El archivo `ios/App/App/Info.plist` incluido en este paquete ya tiene redactadas las justificaciones técnicas que exige Apple (`NSLocationAlwaysAndWhenInUseUsageDescription`) explicando el radar grupal *Pack Ride* y el botón mecánico *SOS 24h*.

---

## 3. Ruta B: Cómo subirla y bajarla en **Google Play Store (Android)**
1. **Crear cuenta en Google Play Console ($25 USD pago único de por vida):**
   - Ingresá en [play.google.com/console](https://play.google.com/console) y creá la aplicación **MotoRuta**.
2. **Generar el archivo `.AAB` (para la tienda) y `.APK` (para instalar ya mismo por WhatsApp):**
   - Ejecutá en tu computadora o mediante la pestaña *Actions* de GitHub:
     ```bash
     npm install
     npx cap sync android
     cd android && ./gradlew bundleRelease assembleRelease
     ```
   - El archivo **`app-release.aab`** se sube a la pista de *Producción* o *Prueba Cerrada* de Google Play Store.
   - El archivo **`app-release.apk`** lo podés mandar hoy mismo por WhatsApp a tu grupo de rodada para instalarlo en 1 toque en cualquier celular Android.
