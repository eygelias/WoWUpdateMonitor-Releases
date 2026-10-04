# WoWUpdateMonitor

App Android que monitorea actualizaciones de builds de World of Warcraft en servidores de Blizzard y envía notificaciones push a teléfonos registrados.

## Qué hace

1. Un **Cloudflare Worker** consulta la API de Blizzard cada pocos minutos.
2. Si detecta un cambio de build (número de versión, build config), manda **FCM** a todos los teléfonos Android registrados.
3. La app Android recibe la notificación, la muestra y la guarda en historial tipo chat.
4. Si hay una nueva versión de la app misma, muestra actualización obligatoria y descarga/instala la APK automáticamente.

## Descargar

Última versión: **v3.1**

[Descargar APK](https://github.com/eygelias/WoWUpdateMonitor-Releases/releases/download/v3.1/WoWUpdateMonitor-v3.1-auto-updater.apk)

[Ver releases](https://github.com/eygelias/WoWUpdateMonitor-Releases/releases)

## Arquitectura

```
Blizzard API → Cloudflare Worker → Firebase FCM → Android App
```

- **Cloudflare Worker**: Consulta builds de WoW (US/EU/CN/KR/TW), detecta cambios, envía FCM
- **Firebase FCM**: Push notifications a teléfonos registrados
- **Android App**: Recibe notificaciones, muestra historial tipo chat, auto-updater

## Funcionalidades

### Monitoreo de versiones
- Consulta Worker periódicamente
- Muestra versiones actuales por juego y región
- Historial de cambios con timestamps

### Notificaciones tipo chat (v3.1)
- Última actualización aparece abajo (estilo WhatsApp)
- Scroll vertical para ver mensajes viejos
- Mantener presionado → menú "Eliminar"
- Historial persistido en SharedPreferences

### Auto-updater (v3.0+)
- Al abrir app, consulta versión actual en GitHub
- Si hay versión mayor → diálogo obligatorio
- Descarga APK desde GitHub dentro de la app
- Botón "Instalar" → abre instalador Android

### Selección de regiones
- US, EU, CN, KR, TW
- Chips Material3 para seleccionar/deseleccionar

## Versión actual

| Campo | Valor |
|---|---|
| versionCode | 4 |
| versionName | 3.1 |
| APK | WoWUpdateMonitor-v3.1-auto-updater.apk |
| Min SDK | 26 (Android 8.0) |
| Target SDK | 34 (Android 14) |

## Requisitos

- Android 8.0+ (API 26)
- Internet

## Changelog

### v3.1
- Chat de notificaciones (última abajo, scroll, eliminar con long press)
- FCM data-only para guardar historial en segundo plano

### v3.0
- Auto-updater: descarga e instala nueva APK desde la app
- Diálogo obligatorio si hay nueva versión
- FileProvider para instalación de APK

### v2.0
- Selección de regiones (US/EU/CN/KR/TW)
- Historial de cambios
- AlarmManager para polling periódico
- BootReceiver para re-registrar alarmas

### v1.0
- Monitoreo básico de versiones
- FCM notifications
- Cloudflare Worker + Firebase

## Código fuente

El código fuente completo está disponible en: [Contexto-WoWUpdateMonitor](https://github.com/eygelias/Contexto-WoWUpdateMonitor)

## Licencia

Código abierto para uso personal y educativo.


---
**SEO Tags:** $tags
