---
name: disenador-nlace
description: >
  Apply NLACE brand design system to every visual output for the agency. Use this skill whenever building, styling, or reviewing any UI, landing page, dashboard, React component, HTML page, artifact, presentation visual, email template, or any frontend piece for NLACE or its products including nlace.com, NLACE AI Studio, cierro, or any client deliverable branded as NLACE. Also trigger when the user mentions NLACE colors, NLACE style, NLACE brand, design system tokens, or asks to make something look like NLACE. This skill overrides generic design defaults with NLACE specific identity including color tokens, typography with Telegraf and Inter, spacing, component patterns, and voice-per-context rules. If anything visual is being produced for NLACE, use this skill first.
---

# Disenador NLACE · v1.8.0

## Fuente de verdad

**Figma (canonica):** https://www.figma.com/design/hboE6NgrEkFXgC9B0M5B18/NLACE-Design-System?node-id=2-1677
- File key: `hboE6NgrEkFXgC9B0M5B18`
- Node raiz: `2:1677`
- 25 secciones documentadas: Logos · Colores · Tipografia · Botones · Inputs · Cards · Badges · Alerts · Navegacion · Hero · Features · Tablas · Tabs · Avatars · Modales · Loaders · Controles · Gradientes · Motion · Espaciado · Radios · Sombras · Focus · Code blocks · tailwind.config

Jerarquia: Figma > SKILL.md. Si hay conflicto, Figma gana siempre.

## Flujo obligatorio por tarea

1. Tareas de fidelidad alta: llamar `Figma:get_variable_defs` (fileKey: `hboE6NgrEkFXgC9B0M5B18`, nodeId: `2:1677`) antes de implementar.
2. Para componentes especificos: llamar `Figma:get_design_context` sobre el nodo del componente.
3. Identificar tipo de producto: marketing / webapp / admin.
4. Mapear requerimiento a tokens y patrones del sistema.
5. Implementar con tokens `--nl-*` (CSS) o clases `nl-*` (Tailwind) antes de crear variantes nuevas.
6. Validar: contraste AA, foco, touch target 44px minimo.
7. Verificar responsive: mobile, tablet, desktop.
8. Entregar resultado + checklist QA de marca.

---

## Tailwind v4 + tokens NLACE

### Setup CDN (prototipos y artifacts)

Tailwind v4 no usa `tailwind.config = {}` — los tokens se definen en CSS con `@theme`.

```html
<!-- CDN Tailwind v4 — development/prototypes only -->
<script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>

<!-- Fuentes -->
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Plus+Jakarta+Sans:wght@700;800&display=swap" rel="stylesheet">

<!-- Material Symbols Outlined (iconos NLACE) -->
<link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200&display=block" rel="stylesheet">

<style type="text/tailwindcss">
@theme {
  /* Colores NLACE */
  --color-nl-bg:           #efefef;
  --color-nl-text:         #141414;
  --color-nl-primary:      #3f58ea;
  --color-nl-primary-dark: #2f2f81;
  --color-nl-accent:       #ff6143;
  --color-nl-accent-warm:  #ff8c42;
  --color-nl-success:      #6be8b0;
  --color-nl-success-dark: #22c55e;
  --color-nl-success-text: #166534;
  --color-nl-success-bg:   #f0fdf4;
  --color-nl-white:        #ffffff;
  --color-nl-900:          #18181b;
  --color-nl-700:          #3f3f46;
  --color-nl-500:          #71717a;
  --color-nl-400:          #a1a1aa;
  --color-nl-border-soft:  #e8e8e8;
  --color-nl-border-ui:    #d4d4d8;
  --color-nl-danger:       #dc2626;
  --color-nl-cyan:         #a5f3fc;
  --color-nl-blue-24:      #1a1a5e;
  --color-nl-blue-28:      #2d1f6e;

  /* Tipografia */
  --font-display: "Plus Jakarta Sans", sans-serif;
  --font-body:    "Inter", sans-serif;
  --font-mono:    "SF Mono", "Fira Code", monospace;

  /* Radios */
  --radius-input: 10px;
  --radius-card:  20px;
  --radius-pill:  9999px;

  /* Sombras */
  --shadow-card:  0 2px 12px rgba(20,20,20,0.08);
  --shadow-hover: 0 10px 28px rgba(20,20,20,0.14);

  /* Letter spacing */
  --tracking-nl-tight:  -0.03em;
  --tracking-nl-normal: -0.018em;
  --tracking-nl-ui:     0.08em;
}
</style>
```

Uso de clases en HTML con v4:
```html
<!-- Colores -->
<div class="bg-nl-primary text-nl-white">...</div>
<div class="bg-nl-accent text-white">...</div>

<!-- Tipografia -->
<h1 class="font-display font-extrabold tracking-nl-tight">...</h1>
<p class="font-body text-nl-700">...</p>

<!-- Gradientes (usar CSS vars directamente en style o @apply) -->
<div style="background: linear-gradient(135deg, #2f2f81 0%, #1a1a5e 60%, #2d1f6e 100%)">...</div>
```

### Setup build (produccion — Vite)

```css
/* main.css */
@import "tailwindcss";

@theme {
  /* mismos tokens de arriba */
}
```

```js
// vite.config.js
import { defineConfig } from "vite";
import tailwindcss from "@tailwindcss/vite";
export default defineConfig({ plugins: [tailwindcss()] });
```

> Nota v4: `tailwind.config.js` no existe en v4. Los plugins JS legacy no corren en CDN — usar CSS nativo o plugins v4.


---

## Iconos — Material Symbols (Google)

NLACE usa **Material Symbols Outlined** como librería de iconos estándar.
Repo: https://github.com/google/material-design-icons
Explorador: https://fonts.google.com/icons

### Import CDN

```html
<!-- Variable font completo (todos los ejes) -->
<link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200&display=block" rel="stylesheet">
```

### Uso en HTML

```html
<!-- Icono básico -->
<span class="material-symbols-outlined">home</span>

<!-- Con CSS personalizado (tamaño, peso, fill) -->
<span class="material-symbols-outlined" style="font-size:20px; font-variation-settings:'wght' 300, 'FILL' 0;">search</span>

<!-- Filled -->
<span class="material-symbols-outlined" style="font-variation-settings:'FILL' 1;">favorite</span>

<!-- Fondo oscuro: grade negativo reduce el brillo -->
<span class="material-symbols-outlined" style="font-variation-settings:'wght' 300, 'FILL' 0, 'GRAD' -25;">star</span>
```

### CSS base recomendado

```css
.material-symbols-outlined {
  font-family: 'Material Symbols Outlined';
  font-weight: normal;
  font-style: normal;
  font-size: 20px;
  line-height: 1;
  display: inline-block;
  white-space: nowrap;
  direction: ltr;
  -webkit-font-smoothing: antialiased;
  font-variation-settings: 'wght' 300, 'FILL' 0, 'GRAD' 0, 'opsz' 20;
}
```

### Configuraciones por contexto NLACE

| Contexto          | opsz | wght | FILL | GRAD | Ejemplo de uso         |
|-------------------|------|------|------|------|------------------------|
| UI pequeño (16px) | 20   | 300  | 0    | 0    | Labels, inputs         |
| UI estándar (24px)| 24   | 300  | 0    | 0    | Botones, listas        |
| Acento / activo   | 24   | 400  | 1    | 0    | Icono activo con color |
| Fondo oscuro      | 24   | 300  | 0    | -25  | Cards oscuras          |
| Hero / portada    | 48   | 200  | 0    | -25  | Decorativos grandes    |

### Iconos frecuentes en UI NLACE

```
Navegación:    home · menu · close · arrow_back · chevron_right
Acciones:      add · edit · delete · search · filter_list · more_vert
Estado:        check_circle · error · warning · info · pending
Contenido:     article · image · attach_file · link · share
IA / tech:     psychology · memory · hub · bolt · auto_awesome
Negocio:       trending_up · bar_chart · people · business · rocket_launch
```


---

## CSS Tokens canonicos (desde Figma node 22)

```css
:root {
  /* Brand colors */
  --nl-bg:           #efefef;
  --nl-text:         #141414;
  --nl-primary:      #3f58ea;
  --nl-primary-dark: #2f2f81;
  --nl-accent:       #ff6143;
  --nl-success:      #6be8b0;

  /* UI support */
  --nl-white:        #ffffff;
  --nl-neutral-900:  #18181b;
  --nl-neutral-700:  #3f3f46;
  --nl-neutral-500:  #71717a;
  --nl-neutral-400:  #a1a1aa;
  --nl-border-soft:  #e8e8e8;
  --nl-border-ui:    #d4d4d8;
  --nl-danger:       #dc2626;
  --nl-success-bg:   #f0fdf4;
  --nl-success-text: #166534;

  /* Acentos adicionales */
  --nl-accent-warm:  #ff8c42;
  --nl-success-dark: #22c55e;
  --nl-cyan:         #a5f3fc;

  /* Opacidades frecuentes */
  --nl-primary-10:   #3f58ea1a;
  --nl-primary-20:   #3f58ea33;
  --nl-accent-10:    #ff61431a;
  --nl-danger-8:     #dc262614;

  /* Radios */
  --nl-radius-input: 10px;
  --nl-radius-card:  20px;
  --nl-radius-pill:  9999px;

  /* Sombras */
  --nl-shadow-card:  0 2px 12px rgba(20,20,20,0.08);
  --nl-shadow-hover: 0 10px 28px rgba(20,20,20,0.14);

  /* Motion */
  --nl-dur-ui:    220ms;
  --nl-dur-reveal: 480ms;
  --nl-ease:      cubic-bezier(0.22, 1, 0.36, 1);

  /* Tipografia */
  --nl-font-display: "Telegraf", "Plus Jakarta Sans", sans-serif;
  --nl-font-body:    "Inter", sans-serif;
  --nl-font-mono:    "SF Mono", "Fira Code", monospace;

  /* Gradientes */
  --nl-grad-hero:       linear-gradient(135deg, #2f2f81 0%, #1a1a5e 60%, #2d1f6e 100%);
  --nl-grad-primary:    linear-gradient(135deg, #3f58ea 0%, #2f2f81 100%);
  --nl-grad-accent:     linear-gradient(135deg, #ff6143 0%, #ff8c42 100%);
  --nl-grad-mint:       linear-gradient(135deg, #6be8b0 0%, #34d399 100%);
  --nl-grad-dark:       linear-gradient(180deg, #18181b 0%, #2f2f81 100%);
  --nl-grad-surface:    linear-gradient(135deg, #ffffff 0%, #f4f4f5 100%);
  --nl-grad-text-brand: linear-gradient(90deg, #3f58ea 0%, #ff6143 100%);
}

body {
  font-family: var(--nl-font-body);
  background: var(--nl-bg);
  color: var(--nl-text);
  -webkit-font-smoothing: antialiased;
}

h1, h2, h3, h4, h5, h6 {
  font-family: var(--nl-font-display);
  letter-spacing: -0.018em;
}

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## Tipografia

| Rol Figma              | Familia          | Peso | Tracking   | Line height |
|------------------------|------------------|------|------------|-------------|
| Plus Jakarta Sans/Bold | Plus Jakarta Sans | 700  | -0.51px    | 40.96px     |
| Inter/Regular          | Inter            | 400  | 0          | 18.43px     |
| Inter/Medium           | Inter            | 500  | 0          | 18.2px      |
| Inter/Bold             | Inter            | 700  | 0          | 19.97px     |
| Inter/Bold upper       | Inter            | 700  | +0.46px    | 18.43px     |

Escala tipografica HTML:

| Tag      | rem    | peso | tracking           |
|----------|--------|------|--------------------|
| H1       | 3.5rem | 800  | -0.03em            |
| H2       | 2.4rem | 800  | -0.025em           |
| H3       | 1.7rem | 700  | -0.02em            |
| H4       | 1.25rem| 700  | -0.015em           |
| Body lg  | 1.1rem | 400  | 0 / lh 1.65        |
| Body     | 0.95rem| 400  | 0 / lh 1.6         |
| Label UI | 0.78rem| 700  | +0.08em uppercase  |
| Caption  | 0.75rem| 400  | 0                  |

Telegraf es comercial. En prototipos y artifacts: `Plus Jakarta Sans`. En produccion: Telegraf auto-hospedado.

---

## Espaciado

Escala canonica px: `4 · 8 · 12 · 16 · 24 · 32 · 48 · 64`

| Token Figma       | px  | Tailwind |
|-------------------|-----|----------|
| item spacing/xs   | 8   | p-2      |
| item spacing/s    | 16  | p-4      |
| item spacing/s+   | 24  | p-6      |
| item spacing/xl   | 64  | p-16     |
| item spacing/5    | 5   | gap-1    |
| item spacing/10   | 10  | gap-2.5  |
| item spacing/15   | 15  | gap-4 ≈  |
| item spacing/40   | 40  | p-10     |

---

## Mapeo Tailwind (artifacts React / HTML)

```
bg-nl-bg                 --nl-bg
text-nl-text             --nl-text
bg-nl-primary            --nl-primary
bg-nl-primary-dark       --nl-primary-dark
bg-nl-accent             --nl-accent (CTA coral)
bg-nl-success            --nl-success (mint)
text-nl-500              --nl-neutral-500
text-nl-400              --nl-neutral-400
bg-nl-900                --nl-neutral-900
border-nl-border-soft    --nl-border-soft
border-nl-border-ui      --nl-border-ui
rounded-input            --nl-radius-input (10px)
rounded-card             --nl-radius-card  (20px)
rounded-pill             --nl-radius-pill  (9999px)
shadow-card              --nl-shadow-card
shadow-hover             --nl-shadow-hover
duration-ui              --nl-dur-ui  (220ms)
duration-reveal          --nl-dur-reveal (480ms)
ease-nl                  --nl-ease
font-display             --nl-font-display
font-body                --nl-font-body
tracking-nl-tight        -0.03em
tracking-nl-normal       -0.018em
tracking-nl-ui           +0.08em
bg-nl-hero               --nl-grad-hero (gradiente azul oscuro)
bg-nl-brand              --nl-grad-text-brand (azul→coral)
```

---

## Componentes — patrones CSS

### Botones

Todos pill. Hover: `translateY(-2px)` + `--nl-shadow-hover`. Coral = marketing. Violeta = producto.

```css
.btn {
  border-radius: var(--nl-radius-pill);
  font-weight: 600;
  transition: transform var(--nl-dur-ui) var(--nl-ease),
              box-shadow var(--nl-dur-ui) var(--nl-ease);
}
.btn:hover    { transform: translateY(-2px); box-shadow: var(--nl-shadow-hover); }
.btn:disabled { opacity: 0.38; transform: none; box-shadow: none; }

/* Variantes */
.btn-accent        { background: var(--nl-accent);   color: #fff; }
.btn-primary       { background: var(--nl-primary);  color: #fff; }
.btn-secondary     { background: var(--nl-white); color: var(--nl-text); border: 1.5px solid var(--nl-border-ui); }
.btn-success       { background: var(--nl-success);  color: var(--nl-success-text); }
.btn-outline-light { background: transparent; color: #fff; border: 1.5px solid rgba(255,255,255,0.5); }

/* Tamaños */
.btn-sm { padding: 7px 16px;  font-size: 0.82rem; }
.btn-md { padding: 11px 22px; font-size: 0.9rem; }
.btn-lg { padding: 15px 30px; font-size: 1rem; }

/* Icon button */
.btn-icon { width: 44px; height: 44px; border-radius: var(--nl-radius-pill); }
```

### Inputs

```css
.form-input, .form-select, .form-textarea {
  min-height: 44px;
  background: var(--nl-white);
  border: 1.5px solid var(--nl-border-ui);
  border-radius: var(--nl-radius-input);
  padding: 0 14px;
  font-family: var(--nl-font-body);
  font-size: 0.9rem;
}
.form-input:focus {
  border-color: var(--nl-primary);
  box-shadow: 0 0 0 4px rgba(63,88,234,0.12);
  outline: none;
}
.form-input.error   { border-color: var(--nl-danger); }
.form-input.success { border-color: var(--nl-success-dark); }
```

### Cards

```css
.card {
  background: var(--nl-white);
  border: 1px solid var(--nl-border-soft);
  border-radius: var(--nl-radius-card);
  box-shadow: var(--nl-shadow-card);
  transition: transform var(--nl-dur-ui) var(--nl-ease),
              box-shadow var(--nl-dur-ui) var(--nl-ease);
}
.card:hover  { transform: translateY(-3px); box-shadow: var(--nl-shadow-hover); }
.card-accent { background: var(--nl-grad-primary); border: none; color: #fff; }
```

### Badges

```css
/* Suaves */
.badge-primary { background: var(--nl-primary-10); color: var(--nl-primary); }
.badge-accent  { background: var(--nl-accent-10);  color: #d64f2a; }
.badge-success { background: rgba(107,232,176,0.2); color: var(--nl-success-text); }
.badge-danger  { background: var(--nl-danger-8);   color: var(--nl-danger); }
.badge-neutral { background: rgba(161,161,170,0.15); color: var(--nl-neutral-700); }

/* Solidos */
.badge-solid-primary { background: var(--nl-primary); color: #fff; }
.badge-solid-accent  { background: var(--nl-accent);  color: #fff; }
.badge-solid-dark    { background: var(--nl-neutral-900); color: #fff; }
```

### Alerts

```css
.alert { border-radius: 14px; padding: 16px 18px; display: flex; gap: 14px; }
.alert-info    { background: rgba(63,88,234,0.08); border-left: 3px solid var(--nl-primary); }
.alert-success { background: var(--nl-success-bg); border-left: 3px solid var(--nl-success-dark); }
.alert-warning { background: #fffbeb; border-left: 3px solid #f59e0b; }
.alert-error   { background: rgba(220,38,38,0.07); border-left: 3px solid var(--nl-danger); }
```

### Tablas

```css
.nl-table { border-collapse: collapse; border-radius: var(--nl-radius-card); overflow: hidden; background: var(--nl-white); }
.nl-table thead th {
  padding: 12px 18px; font-size: 0.72rem; font-weight: 700;
  letter-spacing: 0.07em; text-transform: uppercase;
  color: var(--nl-neutral-400); background: var(--nl-bg);
  border-bottom: 1px solid var(--nl-border-soft);
}
.nl-table tbody tr:hover     { background: rgba(63,88,234,0.03); }
.nl-table.striped tbody tr:nth-child(even) { background: var(--nl-bg); }
.nl-table.compact td, .nl-table.compact th { padding: 8px 14px; font-size: 0.82rem; }
```

### Tabs

```css
/* Underline */
.nl-tab { border-bottom: 2px solid transparent; font-weight: 600; color: var(--nl-neutral-500); padding: 10px 20px; }
.nl-tab.active { color: var(--nl-primary); border-bottom-color: var(--nl-primary); }

/* Pill */
.nl-tabs-pill { background: var(--nl-bg); border-radius: var(--nl-radius-pill); padding: 4px; }
.nl-tab-pill.active { background: var(--nl-white); color: var(--nl-text); box-shadow: 0 1px 4px rgba(20,20,20,0.12); }
```

### Avatars

```css
/* Tamanos: xs=24, sm=32, md=40, lg=56, xl=72 */
.avatar { border-radius: 50%; font-family: var(--nl-font-display); font-weight: 700; color: #fff; }
.avatar-primary { background: var(--nl-primary); }
.avatar-accent  { background: var(--nl-accent); }
.avatar-success { background: var(--nl-success-dark); }
.avatar-dark    { background: var(--nl-neutral-900); }

/* Avatar group */
.avatar-group .avatar { border: 2px solid var(--nl-white); margin-left: -8px; }
```

### Chips

```css
.chip {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 5px 10px 5px 6px;
  background: var(--nl-white); border: 1px solid var(--nl-border-ui);
  border-radius: var(--nl-radius-pill); font-size: 0.82rem; font-weight: 500;
}
```

### Modales

Backdrop con blur. Entrada: `translateY(16px) scale(0.98)` → `translateY(0) scale(1)` en 480ms.

```css
.modal-backdrop { background: rgba(0,0,0,0.45); backdrop-filter: blur(4px); }
.modal {
  background: var(--nl-white);
  border-radius: var(--nl-radius-card);
  box-shadow: var(--nl-shadow-hover);
  animation: modalIn var(--nl-dur-reveal) var(--nl-ease);
}
@keyframes modalIn {
  from { opacity: 0; transform: translateY(16px) scale(0.98); }
  to   { opacity: 1; transform: translateY(0) scale(1); }
}
.modal-destructive .modal-title { color: var(--nl-danger); }
.modal-destructive .btn-confirm { background: var(--nl-danger); color: #fff; }
```

### Progress / Loaders

```css
.progress-track { height: 10px; background: var(--nl-border-soft); border-radius: var(--nl-radius-pill); }
.progress-track.thin { height: 4px; }
.bar-primary  { background: var(--nl-primary); }
.bar-accent   { background: var(--nl-accent); }
.bar-success  { background: var(--nl-success); }
.bar-gradient { background: var(--nl-grad-text-brand); }

/* Spinner */
.spinner {
  border-radius: 50%; border-style: solid;
  border-color: var(--nl-border-ui); border-top-color: var(--nl-primary);
  animation: spin 700ms linear infinite;
}
.spinner-sm { width: 16px; height: 16px; border-width: 2px; }
.spinner-md { width: 24px; height: 24px; border-width: 2.5px; }
.spinner-lg { width: 40px; height: 40px; border-width: 3px; }

/* Skeleton */
.skeleton {
  background: linear-gradient(90deg, var(--nl-border-soft) 25%, var(--nl-bg) 50%, var(--nl-border-soft) 75%);
  background-size: 200% 100%;
  animation: shimmer 1.4s ease-in-out infinite;
  border-radius: 8px;
}
@keyframes spin    { to { transform: rotate(360deg); } }
@keyframes shimmer { 0% { background-position: -200% 0; } 100% { background-position: 200% 0; } }
```

### Toggles / Checkboxes / Radios

```css
/* Toggle */
.nl-toggle { width: 44px; height: 24px; background: var(--nl-border-ui); border-radius: var(--nl-radius-pill); }
.nl-toggle::after { content: ''; width: 18px; height: 18px; background: #fff; border-radius: 50%; transition: transform var(--nl-dur-ui) var(--nl-ease); }
.nl-toggle.on { background: var(--nl-primary); }
.nl-toggle.on::after { transform: translateX(20px); }
.nl-toggle.disabled { opacity: 0.45; }

/* Checkbox */
.nl-checkbox { width: 18px; height: 18px; border: 1.5px solid var(--nl-border-ui); border-radius: 5px; }
.nl-checkbox.checked { background: var(--nl-primary); border-color: var(--nl-primary); color: #fff; }
.nl-checkbox.indeterminate { background: var(--nl-primary); border-color: var(--nl-primary); }

/* Radio */
.nl-radio { width: 18px; height: 18px; border: 1.5px solid var(--nl-border-ui); border-radius: 50%; }
.nl-radio.checked { background: var(--nl-primary); border-color: var(--nl-primary); }
```

### Gradientes — patrones especiales

```css
/* Texto con gradiente — solo en titulares de alto impacto */
.text-gradient {
  background: var(--nl-grad-text-brand);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* Overlay sobre imagen o gradiente */
.overlay-dark {
  background: linear-gradient(to top, rgba(0,0,0,0.55) 0%, rgba(0,0,0,0) 60%);
}
```

### Codigo / Code block

```css
.ds-code {
  background: var(--nl-neutral-900);
  border-radius: 16px;
  padding: 28px;
  font-family: var(--nl-font-mono);
  font-size: 0.8rem;
  line-height: 1.75;
  color: rgba(255,255,255,0.85);
}
```

---

## Hero patterns

### Marketing — gradiente oscuro + coral CTA

```css
.hero-marketing {
  background: var(--nl-grad-hero);
  border-radius: var(--nl-radius-card);
  padding: 64px 56px;
  position: relative; overflow: hidden;
}
/* CTA siempre btn-accent (coral) */
/* Subtitulo: rgba(255,255,255,0.70) */
/* Eyebrow: rgba(255,255,255,0.55), uppercase, tracking 0.12em */
```

**Mesh atmosferico** — patron de fondo para heros de alto impacto:
```css
/* Usar estos radial-gradients sobre --nl-grad-hero */
/* Capa 1 (blur azul izq): radial-gradient(ellipse 60% 50% at 15% 60%, rgba(63,88,234,0.30) 0%, transparent 70%) */
/* Capa 2 (blur coral der): radial-gradient(ellipse 50% 45% at 80% 30%, rgba(255,97,67,0.22) 0%, transparent 65%) */
/* Capa 3 (blur verde centro): radial-gradient(ellipse 40% 35% at 50% 80%, rgba(107,232,176,0.15) 0%, transparent 60%) */
/* En Tailwind: usar style={{ background: '...' }} con los tres radial apilados via coma sobre bg-nl-hero */
```

### Producto — fondo claro + violeta

```css
.hero-product {
  background: var(--nl-white);
  border: 1px solid var(--nl-border-soft);
  border-radius: var(--nl-radius-card);
  box-shadow: var(--nl-shadow-card);
}
/* CTA primario: btn-primary (violeta) */
/* Tag: color var(--nl-primary), uppercase, tracking 0.08em */
```

---

## Motion system

| Patron         | Duracion | Easing              | Uso                              |
|----------------|----------|---------------------|----------------------------------|
| Reveal fadeUp  | 480ms    | ease-out            | Entrada de secciones             |
| Hover elevation| 220ms    | cubic-bezier(0.22,1,0.36,1) | Cards, botones         |
| Pulse ring     | 1.6s     | ease / infinite     | Indicadores de estado activo     |
| Modal in       | 480ms    | nl-ease             | translateY(16px) scale(0.98) → 0 |
| Spinner        | 700ms    | linear / infinite   | Estados de carga                 |

Regla: el movimiento comunica estado, no decora. Siempre soportar `prefers-reduced-motion`.

---

## Dos voces visuales

**Marketing** (landings, ventas, campanas):
- Coral (`--nl-accent`) domina CTAs
- Hero con `--nl-grad-hero` + mesh atmosferico opcional
- Tipografia expresiva, whitespace generoso
- Fondos atmosfericos (gradientes, overlays)

**Producto** (dashboards, admin, tools, apps):
- Violeta (`--nl-primary`) para acciones principales
- Mayor densidad de informacion
- Paleta contenida, foco en claridad operativa
- Cards blancas, tablas, stats

---

## Assets graficos y logos

```
https://nlace.com/hubfs/nlace_black.svg   Wordmark negro (URL publica, fondos claros)
nlace-white.svg          Wordmark blanco (fondos oscuros)
avatar_nlace.svg         App icon / perfil — fondo #5869f7, "n." blanco
logo-nlace-black.png     Email, PDF, print
```

**Avatar real:** fondo azul `#5869f7` con texto `n.` en blanco, tipografia display bold. Dimensiones 1200x1200 (viewBox 900x900). Usar como `<img src="avatar_nlace.svg">` en produccion. En artifacts HTML: embeber PNG base64 extraido del SVG.

### Matriz de decision

| Contexto        | Fondo        | Asset                  | Tailwind fondo         |
|-----------------|--------------|------------------------|------------------------|
| Navbar / header | Claro        | `nlace_black.svg` (nlace.com/hubfs)      | `bg-nl-bg`             |
| Hero / banner   | Oscuro/grad  | `nlace-white.svg`      | `bg-nl-hero`           |
| Footer oscuro   | Dark         | `nlace-white.svg`      | `bg-nl-900`            |
| Footer claro    | Light        | `nlace_black.svg` (nlace.com/hubfs)      | `bg-nl-bg` / `bg-white`|
| Favicon / perfil| Cualquiera   | `avatar_nlace.svg`     | —                      |
| Email signature | Claro        | `logo-nlace-black.png` | —                      |
| Print / PDF     | Blanco       | `nlace_black.svg` (nlace.com/hubfs)      | —                      |

### Tagline

"Innovamos para un mundo que no espera." — uso exclusivo en piezas de marca y presentaciones. No en UI funcional.

### Logo inline SVG — artifacts

```jsx
const NlaceLogoBlack = ({ width = 160, className = "" }) => (
  <svg width={width} height={width * 125/464} viewBox="0 0 464 125" xmlns="http://www.w3.org/2000/svg" className={className}>
    <path d="M0 123.169V34.454H28.965L30.297 52.43l-6.326 2a24.309 24.309 0 0 1 6.492-11.152 34.6 34.6 0 0 1 11.487-7.825 35.391 35.391 0 0 1 13.983-2.83c6.659 0 12.263 1.387 16.813 4.161a24.663 24.663 0 0 1 10.488 12.15c3.553 7.99 4.434 14.537 4.434 26.188v54.594H55.933v-52.1a16.819 16.819 0 0 0-1.332-7.157 9.327 9.327 0 0 0-4-4.494 11.593 11.593 0 0 0-6.326-1.332 16.741 16.741 0 0 0-5.327.832 11.132 11.132 0 0 0-4.162 2.663 11.85 11.85 0 0 0-2.83 3.828 13.35 13.35 0 0 0-.832 4.827v52.929H0Z" fill="#141414"/>
    <path d="M103.929 123.169V0h30.964v123.169h-30.964Z" fill="#141414"/>
    <path d="M183.894 124.667a35.164 35.164 0 0 1-19.81-5.825 42.478 42.478 0 0 1-13.817-16.312 54.7 54.7 0 0 1-4.994-23.8c0-9.099 1.665-17.088 4.994-23.968a39.437 39.437 0 0 1 13.817-16.145 35.285 35.285 0 0 1 20.309-5.992 36.708 36.708 0 0 1 11.32 1.664 26.914 26.914 0 0 1 8.989 4.827 36.936 36.936 0 0 1 6.659 7.157 40.531 40.531 0 0 1 4.661 8.655l-6.325-.333V34.454H240.16v88.715H209.031V101.531l6.825.333a33.93 33.93 0 0 1-11.486 16.312 37.088 37.088 0 0 1-9.323 4.824 35.157 35.157 0 0 1-11.153 1.667Zm8.823-25.466a17.28 17.28 0 0 0 9.156-2.33 15.625 15.625 0 0 0 5.826-7.157 25.864 25.864 0 0 0 2.164-10.985 26.3 26.3 0 0 0-2.164-11.152 14.636 14.636 0 0 0-5.826-6.991 18.037 18.037 0 0 0-18.312 0 14.975 14.975 0 0 0-5.66 6.991 28.2 28.2 0 0 0-2 11.152 27.732 27.732 0 0 0 2 10.985 16.031 16.031 0 0 0 5.66 7.157 17.277 17.277 0 0 0 9.156 2.33Z" fill="#141414"/>
    <path d="M298.074 124.834a46.8 46.8 0 0 1-23.638-5.992 44.24 44.24 0 0 1-16.314-16.312 47.109 47.109 0 0 1-5.993-23.8 46.2 46.2 0 0 1 5.993-23.635 43.875 43.875 0 0 1 16.314-16.478 46.79 46.79 0 0 1 23.638-5.992 60.923 60.923 0 0 1 21.974 3.828A38.016 38.016 0 0 1 336.2 47.437L319.382 67.41a18.918 18.918 0 0 0-4.661-4.161 20.772 20.772 0 0 0-6.326-3 22.581 22.581 0 0 0-7.491-1.165 18.4 18.4 0 0 0-9.655 2.5 17.182 17.182 0 0 0-6.492 6.991 22.041 22.041 0 0 0-2.164 9.987 22.041 22.041 0 0 0 2.164 9.987 17.423 17.423 0 0 0 6.326 6.991A18.357 18.357 0 0 0 300.9 98.2a26.04 26.04 0 0 0 7.491-1 20.933 20.933 0 0 0 6.16-2.829 20.131 20.131 0 0 0 4.827-4.328L336.2 110.186A40.092 40.092 0 0 1 319.882 121 60.448 60.448 0 0 1 298.074 124.834Z" fill="#141414"/>
    <path d="M387.768 124.834c-10.099 0-18.811-1.998-26.135-5.826a42.936 42.936 0 0 1-16.98-16.312 47.106 47.106 0 0 1-5.993-23.8 50.173 50.173 0 0 1 3.329-18.475 43.522 43.522 0 0 1 9.322-14.647 40.178 40.178 0 0 1 14.15-9.654 46.4 46.4 0 0 1 18.145-3.5 44.22 44.22 0 0 1 17.479 3.329 38.271 38.271 0 0 1 13.651 9.487 41.031 41.031 0 0 1 8.823 14.481 46.7 46.7 0 0 1 2.83 18.309l-.167 6.991H356.306l-3.829-15.489h48.941l-3 3.329v-3.162a10.241 10.241 0 0 0-2-6.325 11.85 11.85 0 0 0-4.994-4.328 16.521 16.521 0 0 0-7.158-1.5 17.954 17.954 0 0 0-9.489 2.33 14.314 14.314 0 0 0-5.659 6.325 22.894 22.894 0 0 0-2 9.987 23.429 23.429 0 0 0 2.663 11.485 19.088 19.088 0 0 0 8.157 7.49 30.321 30.321 0 0 0 13.318 2.663 27.386 27.386 0 0 0 8.989-1.332 31.062 31.062 0 0 0 8.49-4.66l14.316 20.14a60.03 60.03 0 0 1-11.819 7.49 58.981 58.981 0 0 1-23.472 5.16Z" fill="#141414"/>
    <path d="M448.352 125c-4.994 0-8.878-1.387-11.653-4.161-2.663-2.774-3.995-6.713-3.995-11.818a15.879 15.879 0 0 1 4.328-11.484 15.006 15.006 0 0 1 11.32-4.494c4.883 0 8.712 1.387 11.486 4.161S464 104.917 464 109.021a15.878 15.878 0 0 1-4.328 11.485A15.006 15.006 0 0 1 448.352 125Z" fill="#141414"/>
  </svg>
);

// Logo blanco: mismos paths, fill="white"

// Avatar: usar <img src="avatar_nlace.svg"> en produccion
// En artifacts sin acceso a archivo: SVG aproximado (fondo #5869f7, "n." blanco)
const NlaceAvatar = ({ size = 40, className = "" }) => (
  <svg width={size} height={size} viewBox="0 0 625 625" xmlns="http://www.w3.org/2000/svg" className={className}>
    <rect width="625" height="625" rx="140" fill="#5869f7"/>
    <text x="50%" y="58%" dominantBaseline="middle" textAnchor="middle"
      fill="white" fontSize="360" fontFamily="Plus Jakarta Sans, sans-serif" fontWeight="800">n.</text>
  </svg>
);
```

---

---


---

## Fotografía corporativa NLACE

Banco de imágenes oficiales: https://lightroom.adobe.com/shares/0d718ea8b724483fa384c6aeeb3c0324

Uso en presentaciones, landing pages, propuestas y cualquier pieza visual de NLACE.

### Criterios de selección

- Preferir fotos con fondo neutro o bokeh suave para composición con texto
- En slides oscuros: fotos con sombras dramáticas o tonos fríos
- En slides claros: fotos con luz natural, ambiente de trabajo
- Nunca recortar rostros en proporciones extrañas — usar aspect-ratio 16/9 o 4/3

### Tratamiento de imagen en diseño

```css
/* Imagen con overlay oscuro para texto encima */
.photo-overlay {
  position: relative;
}
.photo-overlay::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(to right, rgba(20,20,20,0.7) 0%, rgba(20,20,20,0.2) 100%);
}

/* Filtro para coherencia con paleta NLACE */
.photo-nl {
  filter: contrast(1.05) saturate(0.9);
}
```


---

## Presentaciones y documentos

Aplica cuando el output es una presentación (Canva, PPTX) o documento (PDF, propuesta, informe).

### Dirección visual aprobada (validada con Cristian, marzo 2026)

**Estilo:** Tech premium + editorial + minimalismo tenso.
**Base tonal:** Predominantemente claro con slides oscuros como puntos de quiebre estratégicos.

Esta dirección reemplaza el enfoque anterior de "cards sobre fondo gris + rectangulos planos".

---

### Principios de diseño para presentaciones

#### 1. Tipografía como elemento gráfico (NO decorativo)
- Títulos ocupan 60–70% del área útil del slide. No son etiquetas; son el slide.
- Números de stat o de paso: 120–160pt, color primario o blanco, con texto descriptivo pequeño al lado o debajo.
- Palabra o frase clave en coral `#ff6143` dentro del título — rompe la uniformidad y jerarquiza.
- En slides oscuros: texto ghosted gigante como capa de fondo (40–80% opacity, mismo color que fondo pero más claro).

#### 2. Asimetría intencional
- Nada centrado salvo separadores de sección.
- Bloque de color que ocupa exactamente la mitad o un tercio del slide (no porcentajes intermedios como 45%).
- Elementos que se cortan en el borde del slide — encuadre editorial, no poster de PowerPoint.
- Texto que empieza en margen izquierdo y se extiende más allá del centro, empujando el elemento secundario hacia el derecho inferior.

#### 3. Contraste de escala
- En cada slide: un elemento visualmente dominante (tipografía, forma, número) y uno subordinado.
- No mezclar tres elementos del mismo tamaño visual — siempre hay jerarquía clara.
- Cards del mismo tamaño están permitidas solo si son puramente informativas y el titular del slide es el elemento dominante.

#### 4. Profundidad y capas
- Overlays semitransparentes sobre bloques de color (10–25% opacity) para dar profundidad sin complejidad.
- Bordes laterales de acento (4–6px) en slides de contenido claro — coral para servicios, azul para datos.
- Formas geométricas grandes (círculos, rectángulos) fuera del área de texto como elemento de fondo atmosférico.
- Nunca fondo gris plano sin tensión — si el fondo es claro, tiene un elemento de fondo sutil.

#### 5. Estructura de color en el deck (sandwich ampliado)
```
Slide 1         → Oscuro (portada grad-hero)
Slides 2–5      → Claros con accents
Slide 6         → Oscuro (separador de sección)
Slides 7–11     → Claros con accents, 1 slide oscuro de quiebre
Slide 12        → Oscuro (separador)
Slides 13–19    → Claros con accents
Slide 20        → Oscuro (separador o quote)
Slides 21–26    → Claros o mixtos (casos)
Slide 27        → Oscuro (cierre)
```
Regla: nunca más de 4 slides claros consecutivos sin un quiebre oscuro.

---

### Tipos de slide y su layout

| Tipo              | Layout                                             | Fondo                    | Elemento dominante           |
|-------------------|----------------------------------------------------|--------------------------|------------------------------|
| Portada           | Título 60pt+ izquierda, acento en última línea     | grad-hero oscuro          | Tipografía + bloque de color |
| Separador sección | Título 48pt centrado, eyebrow arriba               | `#18181b` o `nl-primary`  | Tipografía                   |
| Contenido texto   | Título 36-44pt izq, cuerpo en columna derecha      | Blanco                   | Título + barra acento lateral|
| Stat / número     | Número 120pt izq o centro, label pequeño debajo    | Blanco o oscuro           | Número gigante               |
| Features 3 col    | Cards con borde-top de color, título bold, 3 líneas body | `#efefef`           | Grid de cards                |
| Split 50/50       | Panel oscuro izq (nombre/tag) + panel claro der (descripción) | Dividido       | Contraste de fondo           |
| Caso / proyecto   | Imagen full-bleed izq (40–50%), texto der con eyebrow + título + body | Blanco | Imagen                  |
| Quote             | Comillas gigantes decorativas, texto 22-26pt, nombre autor pequeño | `#18181b` | Tipografía + comillas |
| Timeline/proceso  | Números grandes + línea superior de color, título + body por columna | Blanco | Números + línea |
| Cierre            | Mismo patrón portada, tagline + contacto           | grad-hero oscuro          | Tipografía                   |

---

### Jerarquia tipografica en slides (pptxgenjs, unidades en pt)

```
Eyebrow / label   8–9pt   · Inter 700 · uppercase · charSpacing 3 · color n500 en claro / rgba(white,0.45) en oscuro
H1 portada        44–52pt · Plus Jakarta Sans 800 (Calibri bold fallback) · charSpacing -0.5
H1 interior       32–40pt · Plus Jakarta Sans 800 · charSpacing -0.4
Título stat       120–160pt · Plus Jakarta Sans 800 · color nl-primary o blanco
H2 subtítulo      20–24pt · Plus Jakarta Sans 700
Body              11–13pt · Inter 400 · lineSpacingMultiple 1.4
Caption / label   9–10pt  · Inter 600
Número de slide   9pt     · Inter regular · opacity 40% · esquina inferior derecha
Ghosted bg text   60–80pt · Plus Jakarta Sans 800 · opacity 8–12% · mismo tono que fondo
```

---

### Paleta por contexto de slide

```
Portada / cierre    → fondo grad-hero (#2f2f81 → #1a1a5e → #2d1f6e) + blobs atmosféricos
Separadores oscuros → fondo #18181b · título blanco · acento coral en eyebrow o divider
Separadores azul    → fondo #3f58ea · título blanco · sin más colores
Contenido claro     → fondo #ffffff · barra lateral coral 5px izq · título #141414
Contenido bg        → fondo #efefef · cards blancas con sombra sutil
Split panel         → panel izq #18181b o #2f2f81 · panel der blanco o #efefef
Stats destacados    → número en #3f58ea o #ff6143 · label en #71717a · fondo blanco
Quote               → fondo #18181b · texto blanco · comillas en #ff6143 muy grandes
```

---

### Reglas de composicion

- Margen seguro: 0.6" en todos los bordes (pptxgenjs en 10"×5.625")
- Nunca más de 3 colores activos por slide (fondo + texto principal + acento)
- Máximo 1 imagen dominante por slide
- Nunca más de 5 bullets — si hay más, partir en 2 slides
- Numeración: esquina inferior derecha, 9pt, color `#a1a1aa`
- Logo: esquina superior izquierda, versión black en fondos claros, versión white en fondos oscuros
- Barra de acento lateral: `x:0, y:0, w:0.055, h:H` — coral para servicios/contenido, azul para datos/metodología
- Shapes decorativas de fondo: usar `transparency: 80–92` para no competir con el contenido
- **Prohibido:** cards con sombra como único elemento visual en un slide sin titular dominante
- **Prohibido:** tres columnas del mismo tamaño sin elemento jerárquico superior de peso visual

---

### Errores del primer deck (pptx v1) — no repetir

Estos errores hicieron que el deck se viera plano y genérico:

1. **Cards como protagonistas** — las cards eran el único elemento visual, sin tipografía dominante encima. Las cards son contenedores de información, no el diseño.
2. **Fondo gris plano `#efefef` sin tensión** — sin shapes de fondo, sin barra lateral, sin contraste de escala. Solo gris con texto.
3. **Todos los slides con el mismo peso visual** — portada, contenido y cierre tenían densidad parecida. No había quiebres oscuros en el medio del deck.
4. **Tipografía conservadora** — títulos de 28–34pt cuando en presentaciones premium van 36–48pt mínimo. El texto no "llenaba" el slide.
5. **Sin elemento ghosted de fondo** — slides oscuros sin texto fantasma ni shape atmosférica. Resultado: oscuro plano.
6. **Asimetría inexistente** — todo alineado a la izquierda al mismo ancho. Sin bloques que rompan el grid.

---

### Voz en presentaciones

- Títulos: afirmativos, sin verbo auxiliar ("Resultados medibles" no "Podemos entregar resultados")
- Subtítulos: una oración, máximo 12 palabras
- Bullets: estructura paralela, arrancar con sustantivo o verbo en presente
- Evitar: "innovador", "disruptivo", "soluciones integrales", "de la mano"
- Tono: directo, técnico-humano, sin hipérboles

---

### Estructura de deck de credenciales NLACE

Basado en Credenciales v5.5 (DAHDFfEoXYQ, 24 slides, enero 2026):

```
1   Portada           → grad-hero + logo blanco + tagline
2   Intro contexto    → quienes somos, 1 parrafo
3   Propuesta valor   → texto centrado, fondo claro
4   Por que NLACE     → stat o quote destacado
5   Eficiencia        → frase + 3 beneficios en columnas
6   Separador lineas  → fondo oscuro, "Nuestras areas"
7   Demand Studio     → card con propuesta de valor + lista servicios
8   Digital Studio    → idem
9   IA Studio         → idem
10  Partners          → logos en grilla sobre fondo claro
11  Etica IA          → texto + 4 principios en columnas, fondo oscuro
12  Separador casos   → "Nuestro dia a dia"
13  Agencia Digital   → caso + descripcion
14  Automatizacion    → caso + descripcion
15  Dashboards        → caso + descripcion
16  Proyectos web     → logos clientes en lista
17  Contenido IA      → caso visual con link
18  Separador metod   → "Nuestra forma de trabajar"
19  Metodologia       → 5 pasos en columnas o timeline
20  Por que nosotros  → 4 razones en grid
21  Separador proyec  → "Ultimos proyectos"
22-26 Casos           → 1 caso por slide: imagen + descripcion
27  Cierre            → grad-hero + tagline + contacto
```

### Canva: brand kit NLACE

Antes de generar presentaciones en Canva, verificar si existe brand kit con `Canva:list-brand-kits`.
Si existe, pasar `brand_kit_id` al generar para aplicar fuentes y colores automaticamente.

## Paquete npm

El design system está publicado como paquete npm instalable en cualquier proyecto.

**npm:** https://www.npmjs.com/package/@nlace/ui-kit
**GitHub:** https://github.com/NLACE-COM/ui-kit

### Instalación

```bash
npm install @nlace/ui-kit
```

### Setup en proyectos Vite / Next.js

```js
// tailwind.config.js
const nlacePreset = require('@nlace/ui-kit/preset')
module.exports = {
  presets: [nlacePreset],
  content: ['./src/**/*.{js,ts,jsx,tsx}', './node_modules/@nlace/ui-kit/dist/**/*.{js,mjs}'],
}

// entry point: main.jsx / _app.tsx / layout.tsx
import '@nlace/ui-kit/tokens'
```

### Componentes disponibles

```js
import { Button, Card, Badge, Input, Alert, NlaceLogo, NlaceAvatar, Spinner, Skeleton } from '@nlace/ui-kit'
```

| Componente   | Variantes principales                                          |
|--------------|----------------------------------------------------------------|
| Button       | accent · primary · secondary · success · outlineLight · danger |
| Card         | default · accent · hover=false                                 |
| Badge        | primary · accent · success · danger · neutral · solid*         |
| Input        | default · error · success · hint                               |
| Alert        | info · success · warning · error                               |
| NlaceLogo    | black · white + prop width                                     |
| NlaceAvatar  | prop size                                                      |
| Spinner      | sm · md · lg                                                   |
| Skeleton     | className para dimensiones                                     |

### Publicar nueva version

```bash
# 1. Bumpar version en package.json
# 2. Build + publish
npm publish

# 3. Tag en GitHub
git tag vX.X.X && git push origin vX.X.X
```

### Estructura del paquete

```
dist/index.mjs        ESM (Vite, Next.js, Claude Code, Codex, etc.)
dist/index.cjs        CommonJS (require)
src/tokens/tokens.css Variables --nl-* + fuentes
src/tailwind-preset.js Preset completo para tailwind.config
```

## QA de marca (ejecutar siempre)

- Tipografia: Telegraf/Plus Jakarta Sans headings, Inter UI/body
- Tokens: sin hex sueltos, todo `var(--nl-*)` o clases `nl-*`
- CTAs: coral (marketing) vs violeta (producto)
- Contraste AA minimo en todos los estados
- Focus ring visible: `box-shadow: 0 0 0 4px rgba(63,88,234,0.12)`
- Touch targets: 44px minimo en mobile
- Estados: hover / active / disabled / focus definidos en componentes interactivos
- Layout responsive sin quiebres en 375px, 768px, 1100px
- Motion: `prefers-reduced-motion` soportado
- Logo correcto segun fondo (claro/oscuro) y contexto
- Avatar: usar imagen real `avatar_nlace.svg`, no inventar gradientes
- Espaciado: escala `4-8-12-16-24-32-48-64`
- Max 1 gradiente dominante por seccion
- Max 1 color de acento dominante por bloque

---

## Evolucion del skill

Despues de cada proyecto:
- Registrar patrones nuevos aprobados en la seccion de componentes.
- Si aparece un token nuevo en Figma: verificar con `Figma:get_variable_defs` y agregar.
- Si se agrega un componente a Figma: leer con `Figma:get_design_context` y documentar patron CSS.
- Objetivo: cero decisiones ad-hoc. Todo tiene origen en Figma.

---

## Versionado

Version actual: `v1.9.0`

- `v1.9.0` - 2026-03-05
  - Sección "Presentaciones y documentos" reescrita con dirección visual aprobada (tech premium + editorial + minimalismo tenso, base clara).
  - 5 principios de diseño documentados: tipografía como elemento gráfico, asimetría intencional, contraste de escala, profundidad y capas, estructura de color en el deck.
  - Tabla de tipos de slide ampliada con stat/número, quote, timeline y split panel.
  - Jerarquía tipográfica actualizada a unidades pptxgenjs con rangos reales probados.
  - Paleta por contexto expandida con split panel y quote oscuro.
  - Sección "Errores del primer deck" agregada como referencia negativa — 6 antipatrones documentados para no repetir.
  - Reglas de composición ampliadas: barra lateral de acento, shapes decorativas, 2 reglas prohibidas explícitas.

- `v1.8.0` - 2026-03-05
  - Tailwind v3 config reemplazado por setup v4 (@theme en CSS, CDN browser@4).
  - Sección "Iconos — Material Symbols" agregada (CDN, CSS base, configuraciones por contexto, iconos frecuentes NLACE).
  - Sección "Fotografía corporativa NLACE" agregada con link al banco Adobe Lightroom y criterios de uso.

- `v1.7.0` - 2026-03-05
  - Seccion "Presentaciones y documentos" agregada al skill.
  - Tipos de slide, jerarquia tipografica, paleta por contexto, reglas de composicion y voz.
  - Estructura canonica del deck de credenciales NLACE (24 slides) documentada como referencia.
  - Guia de Canva: verificar brand kit antes de generar presentaciones.

- `v1.6.0` - 2026-03-05
  - Paquete npm publicado: `@nlace/ui-kit` en https://www.npmjs.com/package/@nlace/ui-kit
  - GitHub: https://github.com/NLACE-COM/ui-kit
  - Componentes compilados en ESM + CJS (dist/). Compatible con Claude Code, Codex, Antigravity y cualquier entorno sin build step.
  - Logo negro: URL publica https://nlace.com/hubfs/nlace_black.svg
  - Seccion "Paquete npm" agregada al skill con tabla de componentes, setup y flujo de publicacion.

- `v1.5.0` - 2026-03-05
  - Tailwind config canonico documentado completo (colores, fontFamily, borderRadius, boxShadow, timing, gradients, animations, keyframes, letterSpacing).
  - Mapeo Tailwind ampliado con todas las clases `nl-*` del UI Kit.
  - Hero mesh atmosferico documentado: 3 capas radial-gradient sobre `--nl-grad-hero`.
  - Seccion logos actualizada: avatar real es `avatar_nlace.svg` con fondo `#5869f7` (no inventar gradientes).
  - NlaceAvatar corregido: `fill="#5869f7"` en lugar de `#3f58ea`.
  - Secciones del sistema actualizadas de 22 a 25 (+ Focus, Code blocks, tailwind.config).
  - QA ampliado: regla explicita de no inventar gradientes en avatares.

- `v1.4.0` - 2026-03-03
  - Patrones CSS documentados para los 22 modulos del design system Figma.
  - Tokens de sombra, opacidad, ease canonico y motion system completo.

- `v1.3.0` - 2026-03-03
  - Conexion directa al archivo Figma.
  - Tokens sincronizados con nombres canonicos de variables Figma.

- `v1.2.0` - 2026-03-02
  - Merge nlace-designer: tokens inline, mapeo Tailwind, fallback tipografico, SVG logos.

- `v1.1.0` - 2026-03-02
  - Assets graficos y matriz de logos por contexto.

- `v1.0.0` - 2026-02-26
  - Creacion inicial.
