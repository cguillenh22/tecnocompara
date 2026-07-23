---
layout: default
title: "Contacto"
description: "Escríbenos si encontraste un error, tienes una sugerencia o quieres reportar un enlace roto."
permalink: /contacto/
---
<div class="container article-body" style="max-width:640px; padding-top:32px;" markdown="1">

# Contacto

¿Encontraste un error en algún artículo, un enlace roto, o quieres
sugerir una comparativa? Escríbenos con el formulario de abajo — leemos
todos los mensajes.

<form action="https://formspree.io/f/xgogzwag" method="POST" style="margin-top:24px;">
  <div style="margin-bottom:16px;">
    <label for="name" style="display:block; font-family:var(--font-mono); font-size:0.75rem; text-transform:uppercase; letter-spacing:0.05em; color:var(--color-ink-soft); margin-bottom:6px;">Nombre</label>
    <input type="text" id="name" name="name" required style="width:100%; padding:10px 12px; border:1px solid var(--color-line-strong); border-radius:4px; font-family:var(--font-body); font-size:1rem;">
  </div>
  <div style="margin-bottom:16px;">
    <label for="email" style="display:block; font-family:var(--font-mono); font-size:0.75rem; text-transform:uppercase; letter-spacing:0.05em; color:var(--color-ink-soft); margin-bottom:6px;">Correo</label>
    <input type="email" id="email" name="email" required style="width:100%; padding:10px 12px; border:1px solid var(--color-line-strong); border-radius:4px; font-family:var(--font-body); font-size:1rem;">
  </div>
  <div style="margin-bottom:16px;">
    <label for="motivo" style="display:block; font-family:var(--font-mono); font-size:0.75rem; text-transform:uppercase; letter-spacing:0.05em; color:var(--color-ink-soft); margin-bottom:6px;">Motivo</label>
    <select id="motivo" name="motivo" required style="width:100%; padding:10px 12px; border:1px solid var(--color-line-strong); border-radius:4px; font-family:var(--font-body); font-size:1rem;">
      <option value="">Selecciona una opción</option>
      <option value="Error en artículo">Reportar un error en un artículo</option>
      <option value="Enlace roto">Reportar un enlace roto</option>
      <option value="Sugerencia de comparativa">Sugerir una comparativa</option>
      <option value="Otro">Otro</option>
    </select>
  </div>
  <div style="margin-bottom:20px;">
    <label for="message" style="display:block; font-family:var(--font-mono); font-size:0.75rem; text-transform:uppercase; letter-spacing:0.05em; color:var(--color-ink-soft); margin-bottom:6px;">Mensaje</label>
    <textarea id="message" name="message" rows="6" required style="width:100%; padding:10px 12px; border:1px solid var(--color-line-strong); border-radius:4px; font-family:var(--font-body); font-size:1rem; resize:vertical;"></textarea>
  </div>
  <input type="text" name="_gotcha" style="display:none">
  <button type="submit" class="cta-afiliado" style="border:none; cursor:pointer;">Enviar mensaje →</button>
</form>

</div>
