# Idea: Web Player Propio (tipo miralotv)

## Concepto
Crear una página web hospedada en **GitHub Pages** (gratis) que funcione como player
de los canales del repo, usando hls.js + CDNBye P2P Engine.

## Stack técnico
- **GitHub Pages** → hosting gratuito
- **hls.js** → reproductor HLS en navegador
- **@swarmcloud/hls (CDNBye)** → P2P engine para reducir ancho de banda si hay múltiples viewers
- **Tu mis_canales.m3u** → fuente de canales

## Código base

```html
<!DOCTYPE html>
<html>
<head>
  <title>Mi TV</title>
  <script src="https://cdn.jsdelivr.net/npm/@swarmcloud/hls/p2p-engine.min.js"></script>
</head>
<body>
  <video id="player" controls autoplay width="100%"></video>
  <script>
    const video = document.getElementById('player');
    const hls = new Hls({ p2pConfig: { logLevel: 'warn' } });

    // Cargar canal (reemplazar con URL del stream deseado)
    hls.loadSource('https://origin.dpsgo.com/ssai/event/GI-9cp_bT8KcerLpZwkuhw/master.m3u8');
    hls.attachMedia(video);
  </script>
</body>
</html>
```

## Instalación CDNBye (npm)
```bash
npm install --save @swarmcloud/hls
```

## Para verlo en LG TV
- Abrir el browser del LG TV (no SmartOne)
- Navegar a: `https://maldoxs.github.io/mi-iptv-personal`

## Notas importantes
- P2P solo da beneficio si múltiples personas ven el mismo canal al mismo tiempo
- Para uso personal (1 viewer), el P2P no aporta nada
- GitHub Pages requiere que el repo sea público (ya lo es)
- Requiere registrar el dominio en https://docs.swarmcloud.net para activar P2P

## Fuentes
- Repo CDNBye: https://github.com/cdnbye/hlsjs-p2p-engine
- Docs: https://docs.swarmcloud.net/web-hls
- Demo: https://demo.cdnbye.com
