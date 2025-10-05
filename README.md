# mi-sitio-fotos---
title: Overview · Cloudflare Pages docs
description: Deploy your Pages project by connecting to your Git provider,
  uploading prebuilt assets directly to Pages with Direct Upload or using C3
  from the command line.
lastUpdated: 2025-09-15T21:45:20.000Z
chatbotDeprioritize: false
source_url:
  html: https://developers.cloudflare.com/pages/
  md: https://developers.cloudflare.com/pages/index.md
---

Create full-stack applications that are instantly deployed to the Cloudflare global network.

Available on all plans

Deploy your Pages project by connecting to [your Git provider](https://developers.cloudflare.com/pages/get-started/git-integration/), uploading prebuilt assets directly to Pages with [Direct Upload](https://developers.cloudflare.com/pages/get-started/direct-upload/) or using [C3](https://developers.cloudflare.com/pages/get-started/c3/) from the command line.

***

## Features

### Pages Functions

Use Pages Functions to deploy server-side code to enable dynamic functionality without running a dedicated server.

[Use Pages Functions](https://developers.cloudflare.com/pages/functions/)

### Rollbacks

Rollbacks allow you to instantly revert your project to a previous production deployment.

[Use Rollbacks](https://developers.cloudflare.com/pages/configuration/rollbacks/)

### Redirects

Set up redirects for your Cloudflare Pages project.

[Use Redirects](https://developers.cloudflare.com/pages/configuration/redirects/)

***

## Related products

**[Workers](https://developers.cloudflare.com/workers/)**

Cloudflare Workers provides a serverless execution environment that allows you to create new applications or augment existing ones without configuring or maintaining infrastructure.

**[R2](https://developers.cloudflare.com/r2/)**

Cloudflare R2 Storage allows developers to store large amounts of unstructured data without the costly egress bandwidth fees associated with typical cloud storage services.

**[D1](https://developers.cloudflare.com/d1/)**

D1 is Cloudflare’s native serverless database. Create a database by importing data or defining your tables and writing your queries within a Worker or through the API.

**[Zaraz](https://developers.cloudflare.com/zaraz/)**

Offload third-party tools and services to the cloud and improve the speed and security of your website.

***

## More resources

[Limits](https://developers.cloudflare.com/pages/platform/limits/)

Learn about limits that apply to your Pages project (500 deploys per month on the Free plan).

[Framework guides](https://developers.cloudflare.com/pages/framework-guides/)

Deploy popular frameworks such as React, Hugo, and Next.js on Pages.

[Developer Discord](https://discord.cloudflare.com)

Connect with the Workers community on Discord to ask questions, show what you are building, and discuss the platform with other developers.

[@CloudflareDev](https://x.com/cloudflaredev)

Follow @CloudflareDev on Twitter to learn about product announcements, and what is new in Cloudflare Workers.
<!doctype html>

<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Sitio de Fotos - Galería</title>
  <meta name="description" content="Galería de imágenes simple y gratuita. Sustituye las imágenes en la carpeta /images o usa URLs directas." />
  <style>
    /* --- Estilos básicos (modifica libremente) --- */
    :root{--bg:#0f1724;--card:#0b1220;--accent:#7dd3fc;--text:#e6eef8}
    *{box-sizing:border-box}
    body{margin:0;font-family:Inter, system-ui, Arial, sans-serif;background:linear-gradient(180deg,#071021 0%, #0f1724 100%);color:var(--text);min-height:100vh;display:flex;flex-direction:column}
    header{padding:18px 20px;display:flex;align-items:center;gap:12px}
    .brand{display:flex;flex-direction:column}
    h1{margin:0;font-size:1.1rem}
    p.lead{margin:0;color:#9fb6c9;font-size:0.9rem}main{padding:12px 20px;flex:1}
.controls{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:12px}
.btn{background:transparent;border:1px solid rgba(255,255,255,0.06);padding:8px 12px;border-radius:10px;color:var(--text);cursor:pointer}

/* Galería */
.gallery{display:grid;grid-template-columns:repeat(auto-fill,minmax(160px,1fr));gap:10px}
.card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border-radius:12px;overflow:hidden;position:relative;cursor:pointer}
.card img{width:100%;height:160px;object-fit:cover;display:block}
.caption{position:absolute;left:8px;bottom:8px;padding:6px 8px;border-radius:8px;background:rgba(0,0,0,0.4);font-size:0.8rem}

/* Modal Lightbox */
.lightbox{position:fixed;inset:0;background:rgba(0,0,0,0.75);display:none;align-items:center;justify-content:center;padding:20px}
.lightbox.open{display:flex}
.lightbox img{max-width:95%;max-height:85%;border-radius:8px;box-shadow:0 10px 30px rgba(0,0,0,0.6)}
.close-btn{position:absolute;right:18px;top:18px;padding:8px;border-radius:50%;background:rgba(255,255,255,0.06);border:none;color:var(--text);cursor:pointer}

/* Upload area */
.uploader{border:2px dashed rgba(255,255,255,0.04);padding:12px;border-radius:10px;text-align:center}
.uploader.dragover{background:linear-gradient(90deg, rgba(255,255,255,0.01), rgba(125,211,252,0.02));border-color:rgba(125,211,252,0.15)}
input[type=file]{display:none}

footer{padding:12px 20px;color:#93aec3;font-size:0.85rem;text-align:center}

@media (min-width:900px){
  .card img{height:200px}
}

  </style>
</head>
<body>
  <!--
    INSTRUCCIONES RÁPIDAS:
    - Para usar tu propia galería, sustituye las etiquetas <img src="..."> dentro de <div class="gallery"> por las rutas de tus imágenes.
    - Si subes imágenes a un hosting (GitHub Pages, Netlify, Google Drive público, etc.), pega la URL completa en el atributo src.
    - Para publicar gratis: sube este archivo a GitHub y activa GitHub Pages, o súbelo a Netlify/Cloudflare Pages siguiendo sus guías.
    - Si quieres que lo personalice (cambiar colores, añadir un formulario de contacto, dominio gratis), dime y lo hago.
  -->  <header>
    <div style="width:48px;height:48px;border-radius:10px;background:linear-gradient(135deg,var(--accent),#60a5fa);display:flex;align-items:center;justify-content:center;font-weight:700;color:#012">F</div>
    <div class="brand">
      <h1>Sitio de Fotos</h1>
      <p class="lead">Galería rápida y responsive — toca una imagen para verla grande.</p>
    </div>
  </header>  <main>
    <div class="controls">
      <label class="btn" for="fileInput">Subir imágenes</label>
      <button class="btn" id="clearBtn">Limpiar galería</button>
      <button class="btn" id="downloadBtn">Descargar lista</button>
    </div><div class="uploader" id="uploader">
  Arrastra y suelta imágenes aquí, o haz clic en "Subir imágenes".
  <input id="fileInput" type="file" accept="image/*" multiple />
</div>

<section class="gallery" id="gallery">
  <!-- Ejemplos: reemplaza estas imágenes por las tuyas -->
  <div class="card"><img src="https://images.unsplash.com/photo-1503023345310-bd7c1de61c7d?q=80&w=800&auto=format&fit=crop" alt="Foto 1"><div class="caption">Playa</div></div>
  <div class="card"><img src="https://images.unsplash.com/photo-1472214103451-9374bd1c798e?q=80&w=800&auto=format&fit=crop" alt="Foto 2"><div class="caption">Montaña</div></div>
  <div class="card"><img src="https://images.unsplash.com/photo-1454496522488-7a8e488e8606?q=80&w=800&auto=format&fit=crop" alt="Foto 3"><div class="caption">Ciudad</div></div>
  <div class="card"><img src="https://images.unsplash.com/photo-1491553895911-0055eca6402d?q=80&w=800&auto=format&fit=crop" alt="Foto 4"><div class="caption">Retrato</div></div>
</section>

  </main>  <footer>
    Hecho con ❤️. Puedes editar este archivo y subirlo a GitHub Pages o Netlify para publicarlo gratis.
  </footer>  <!-- Lightbox -->  <div id="lightbox" class="lightbox" aria-hidden="true">
    <button class="close-btn" id="closeLight">✕</button>
    <img id="lightboxImg" src="" alt="Imagen ampliada">
  </div>  <script>
    // Funcionalidad: lightbox, subir imágenes en el navegador (client-side preview), descargar lista de URLs.
    const gallery = document.getElementById('gallery');
    const lightbox = document.getElementById('lightbox');
    const lbImg = document.getElementById('lightboxImg');
    const closeLight = document.getElementById('closeLight');
    const fileInput = document.getElementById('fileInput');
    const uploader = document.getElementById('uploader');
    const clearBtn = document.getElementById('clearBtn');
    const downloadBtn = document.getElementById('downloadBtn');

    
