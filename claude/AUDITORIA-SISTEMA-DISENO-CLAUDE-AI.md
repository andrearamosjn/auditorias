# Auditoría de Sistema de Diseño — claude.ai

**Fecha:** 12–16 de febrero de 2026
**Auditor:** Claude (automatizado vía Playwright)
**Versión analizada:** claude.ai (web app, plan gratuito)
**Última actualización:** 16 de febrero de 2026

---

## 1. Pantallas Auditadas

| # | Pantalla | Archivo |
|---|----------|---------|
| 1 | Home / Nueva conversación (sidebar colapsada) | `01-home-new-chat.png` |
| 2 | Home (sidebar expandida) | `02-sidebar-expanded.png` |
| 3 | Lista de Chats | `03-chats-list.png` |
| 4 | Proyectos (estado vacío) | `04-projects.png` |
| 5 | Artefactos (galería de inspiración) | `05-artifacts.png` |
| 6 | Menú de perfil (dropdown) | `06-profile-menu.png` |
| 7 | Ajustes > General | `07-settings-general.png` |
| 8 | Ajustes > General (modo oscuro) | `08-settings-dark-mode.png` |
| 9 | Ajustes > Cuenta | `09-settings-account.png` |
| 10 | Página de Upgrade / Planes | `10-upgrade-plans.png` |
| 11 | Conversación de chat | `11-chat-conversation.png` |
| 12 | Categoría de prompts (Crear) | `12-prompt-category-crear.png` |
| 13 | Verificación de seguridad (Cloudflare) | `13-login.png` |
| 14 | Chat con bloque de código (syntax highlighting) | `14-chat-code-block.png` |
| 15 | Selector de modelo (dropdown) | `15-model-selector.png` |
| 16 | Menú de adjuntos / upload | `16-attachment-menu.png` |
| 17 | Modal de confirmación (eliminar chat) | `17-delete-confirmation-modal.png` |
| 18 | Sidebar con hover states | `18-sidebar-hover-states.png` |
| 19 | Categoría de prompts (Código) | `19-prompt-category-codigo.png` |
| 20 | Modal de búsqueda (Cmd+K) | `20-search-modal.png` |
| 21 | Menú contextual de chat (3 puntos) | `17-chat-context-menu.png` |
| 22 | Dialog promocional (Cowork) | `19-cowork-promo-dialog.png` |

---

## 1b. Pantalla de entrada: Verificación de seguridad (Cloudflare)

**Archivo:** `13-login.png`

Esta es la primera pantalla que ve cualquier usuario al acceder a claude.ai. Es una página de Cloudflare Turnstile (challenge anti-bot) que actúa como puerta de entrada antes de la app.

### Análisis de diseño

| Elemento | Valor | Observación |
|----------|-------|-------------|
| **Fondo** | `#FFFFFF` (blanco puro) | **Rompe** con el crema `#FAF9F5` de la app |
| **Logo** | Asterisco terracota + "claude.ai" | Tipografía sans-serif, peso medio, ~40px |
| **Título** | "Verificación de seguridad en curso" | Negro, bold, ~20px |
| **Cuerpo** | Texto descriptivo | Gris oscuro, ~16px, buena legibilidad |
| **Widget** | Cloudflare Turnstile | Caja con borde, "Verificando...", logo Cloudflare |
| **Footer** | Ray ID + links Cloudflare/Privacidad | Texto centrado, gris, ~12px |
| **Layout** | Contenido alineado izquierda, centrado vertical parcial | Mucho espacio vacío debajo |

### Hallazgos

- **Inconsistencia de fondo:** El blanco puro `#FFFFFF` contrasta con el crema cálido `#FAF9F5` que el usuario verá inmediatamente después. La transición puede ser perceptible.
- **Sin branding extendido:** Solo el logo asterisco + nombre. No hay ilustración, color de marca ni calidez visual. La primera impresión es fría y genérica.
- **Fuera del control del design system:** Esta página la sirve Cloudflare, no la app de Claude. Es difícil personalizarla, aunque Cloudflare Turnstile permite cierta customización de tema.
- **i18n correcto:** El texto está en español, consistente con el idioma del navegador.
- **UX de espera:** No hay indicador de progreso claro más allá del spinner del widget. En conexiones lentas puede generar incertidumbre.

---

## 2. Tipografía

### Familias tipográficas

| Token CSS | Valor | Uso |
|-----------|-------|-----|
| `--font-ui` | `anthropicSans` (custom) | UI general, sidebar, botones, inputs |
| `--font-ui-serif` | `anthropicSerif` (custom) | Respuestas de Claude |
| `--font-claude-response` | `var(--font-anthropic-serif)` | Texto de respuesta del asistente |
| `--font-user-message` | `var(--font-ui)` | Mensajes del usuario |
| `--font-mono` | `JetBrains Mono` (custom) | Código |
| `--font-system` | `system-ui, sans-serif` | Opción "Sistema" en ajustes |
| `--font-dyslexia` | `OpenDyslexic, Comic Sans MS, ui-serif` | Modo adaptado para dislexia |

**Fallbacks del body:** `anthropicSans, "anthropicSans Fallback", system-ui, "Segoe UI", Roboto, Helvetica, Arial, sans-serif`

### Escala tipográfica

| Elemento | Font Size | Font Weight | Line Height | Uso |
|----------|-----------|-------------|-------------|-----|
| H1 (página) | 30px | 500 | 36px | Títulos principales ("Planes que crecen contigo") |
| H1 (hero home) | ~36-40px | 400 | — | Saludo personalizado |
| H2 (settings) | ~20px | 500 | — | Secciones de ajustes |
| H3 | 24px | 500 | 32px | Cards de planes, títulos de sección |
| Body / UI | 16px | 400-430 | 24px | Texto general |
| Botones | 14px | 430-500 | 19.6px | CTAs, acciones |
| Captions / labels | 12px | 400-500 | 16px | Etiquetas sidebar, timestamps, pills |

### Observaciones tipográficas

- **Peso variable:** Se usa `font-weight: 430` extensivamente (no es un peso estándar), indica uso de fuente variable.
- **Consistencia:** La fuente `anthropicSans` se usa de forma homogénea en toda la UI. Serif solo para respuestas de Claude.
- **Accesibilidad positiva:** Ofrecen 4 opciones de fuente incluyendo modo para dislexia (OpenDyslexic).

---

## 3. Paleta de Colores

### Modo Claro (Básica)

#### Fondos

| Color | RGB | Uso |
|-------|-----|-----|
| Crema cálido (base) | `rgb(250, 249, 245)` / `#FAF9F5` | Fondo principal del body |
| Crema medio | `rgb(240, 238, 230)` / `#F0EEE6` | Sidebar hover, separadores |
| Blanco puro | `rgb(255, 255, 255)` / `#FFFFFF` | Cards de planes, inputs |
| Negro casi puro | `rgb(20, 20, 19)` / `#141413` | Botones CTA primarios |

#### Textos

| Color | RGB | Uso |
|-------|-----|-----|
| Negro primario | `rgb(20, 20, 19)` / `#141413` | Títulos, texto principal |
| Gris oscuro | `rgb(61, 61, 58)` / `#3D3D3A` | Texto secundario, mensajes de usuario |
| Gris medio | `rgb(115, 114, 108)` / `#73726C` | Labels, placeholders, texto terciario |
| Blanco | `rgb(255, 255, 255)` | Texto sobre botones oscuros |

#### Acentos

| Color | RGB | Uso |
|-------|-----|-----|
| Azul link | `rgb(44, 132, 219)` / `#2C84DB` | Links activos, acento de selección |
| Azul oscuro | `rgb(27, 103, 178)` / `#1B67B2` | Links hover, sombras de acento |
| Naranja/terracota | *(icono Claude)* | Solo en el logotipo asterisco |

#### Bordes

| Color | Uso |
|-------|-----|
| `rgba(31, 30, 29, 0.15)` | Bordes sutiles de cards |
| `rgba(31, 30, 29, 0.3)` | Bordes de inputs, botones outline |
| `rgba(31, 30, 29, 0.4)` | Bordes más marcados |
| `rgba(44, 132, 219, 0.4)` | Borde de focus / acento azul |

### Modo Oscuro

- Inversión completa: fondos pasan a tonos oscuros/negros
- Textos se invierten a blancos/grises claros
- Mantiene el mismo sistema de opacidades para bordes
- Toggle de switch usa blanco sobre fondo oscuro

### Hallazgos de color

- **Paleta muy restringida y coherente:** Solo 4 colores de fondo y 4 de texto en toda la app.
- **Tono cálido diferenciador:** El crema `#FAF9F5` como fondo base le da personalidad frente al blanco puro típico.
- **Buen contraste:** Negro `#141413` sobre crema `#FAF9F5` tiene un ratio de contraste excelente (~18:1).
- **Problema menor:** El gris `#73726C` sobre crema `#FAF9F5` puede estar al límite del ratio 4.5:1 WCAG AA para texto pequeño.

---

## 4. Espaciado y Layout

### Grid y Layout

- **Sidebar:** Ancho fijo ~300px expandida, ~56px colapsada (solo iconos)
- **Contenido principal:** Centrado con `max-width` contenido, se expande a pantalla completa
- **Chat:** Layout vertical con mensajes alineados a la izquierda (asistente) y derecha (usuario)

### Sistema de espaciado

- Espaciado base en múltiplos de **4px** y **8px**
- Padding de botones: `24px 16px` (CTA grande), `4px 10px` (pill), `0px` (ghost)
- Padding de chat messages: `32px 16px`
- Gaps entre items de sidebar: `4px`

---

## 5. Componentes UI

### 5.1 Botones

| Variante | Background | Color | Border | Radius | Ejemplo |
|----------|-----------|-------|--------|--------|---------|
| **Primario (CTA)** | `#141413` | blanco | ninguno | 12px | "Obtener Plan Pro" |
| **Outline** | transparente | `#141413` | `0.5px solid rgba(31,30,29,0.3)` | 12px | "Usa Claude gratis" |
| **Ghost** | transparente | `#141413` | ninguno | 6px | Sidebar items |
| **Pill** | `#FAF9F5` o transparente | texto | ninguno | 9999px | "Anual", "Mensual" |
| **Destructivo** | `#141413` | blanco | ninguno | — | "Eliminar cuenta" |
| **Tab/Chip** | transparente | texto | outline sutil | 8px | "Crear", "Aprender" |

**Observaciones:**
- No hay botón rojo de peligro; "Eliminar cuenta" usa el mismo estilo que CTA primario (negro), lo que puede causar confusión UX.
- Los botones ghost no tienen padding, dependen del contenedor padre.

### 5.2 Inputs y Formularios

| Componente | Estilo |
|-----------|--------|
| **Textbox de chat** | Sin borde visible, fondo transparente sobre card blanca con sombra sutil |
| **Search input** | Borde con focus azul (`rgba(44,132,219,0.4)`), icono de lupa |
| **Text input (settings)** | Borde sutil, fondo ligeramente distinto |
| **Combobox/Select** | Borde sutil, flecha dropdown |
| **Textarea (preferences)** | Borde sutil, placeholder en gris |
| **Switch/Toggle** | Estilo estándar, sin personalización especial |

### 5.3 Cards

- **Cards de planes:** Fondo blanco, border radius 16px, sombra `rgba(0,0,0,0.04) 0px 2px 8px`
- **Card Pro destacada:** Sombra más intensa `rgba(0,0,0,0.05) 0px 6px 22px`, borde azul
- **Cards de artefactos:** Grid de thumbnails con imágenes, radius 8-10px, label debajo

### 5.4 Navegación

- **Sidebar:** Colapsable, iconos SVG personalizados, items con hover sutil en crema
- **Tabs de categorías:** Row de chips/pills con icono + texto
- **Settings nav:** Lista vertical de links, item activo con fondo crema
- **Breadcrumbs/tabs de artefactos:** "Inspiración" / "Tus artefactos" con underline activo

### 5.5 Menú contextual (Dropdown)

- Fondo blanco, sombra suave
- Items con icono + texto + atajo de teclado opcional
- Separadores horizontales para agrupar secciones
- Corner radius consistente

### 5.6 Chat Messages

| Elemento | Estilo |
|----------|--------|
| **Mensaje de usuario** | Alineado derecha, fondo gris/crema oscuro, pill redondeada |
| **Mensaje de asistente** | Alineado izquierda, sin fondo, tipografía serif |
| **Acciones de mensaje** | Iconos: copiar, like, dislike, retry |
| **Icono Claude** | Asterisco naranja/terracota |
| **Input de respuesta** | Card flotante con sombra, botón +, selector de modelo, botón de voz |

---

## 6. Iconografía

- **Sistema de iconos:** SVG inline personalizados, estilo outlined/line
- **Grosor de trazo:** Consistente, fino (~1.5-2px)
- **Tamaños:** ~16px en sidebar, ~20px en acciones de chat
- **Iconos destacados:**
  - Asterisco Claude (marca, color terracota)
  - Sidebar: +, chat, carpeta, grid, código, toggle
  - Chat: copiar, pulgar arriba/abajo, refresh
  - Settings: engranaje, mundo, ayuda, regalo, descarga, info, logout

---

## 7. Sombras y Elevación

| Nivel | Valor | Uso |
|-------|-------|-----|
| Nivel 0 | Ninguna | Mayoría de elementos |
| Nivel 1 | `rgba(0,0,0,0.05) 0px 1px 2px` | Sombra sutil |
| Nivel 2 | `rgba(0,0,0,0.04) 0px 2px 8px` | Cards estándar |
| Nivel 3 | `rgba(0,0,0,0.05) 0px 6px 22px` | Card destacada (Pro) |
| Acento | `rgba(27,103,178,0.1) 0px 4px 24px` | Glow azul en card Pro |
| Acento 2 | `rgba(44,132,219,0.16) 0px 2px 8px` | Focus azul |

**Observaciones:** Sistema de elevación muy sutil y contenido, coherente con la estética minimalista cálida.

---

## 8. Border Radius

| Valor | Uso |
|-------|-----|
| `6px` | Botones ghost, elementos pequeños |
| `8px` | Tabs, chips, pills de navegación |
| `10px` | Cards de artefactos |
| `12px` | Botones CTA, inputs |
| `16px` | Cards de planes grandes |
| `9999px` | Pills, toggles, avatares |

---

## 9. Accesibilidad

### Positivo
- **Roles ARIA correctos:** `navigation`, `main`, `tablist`, `tab`, `tabpanel`, `listbox`, `option`, `menu`, `menuitem`, `switch`, `alert`, `status`, `region`
- **Labels descriptivos:** Sidebar tiene `aria-label="Barra lateral"`, notificaciones tienen `aria-label="Notificaciones (F8)"`
- **Atajos de teclado:** Documentados visualmente (Ctrl+Shift+O, Shift+Cmd+,)
- **Modo dislexia:** Opción de fuente OpenDyslexic
- **Nota de IA:** Disclaimer visible "Claude es IA y puede cometer errores"
- **Soporte i18n:** Interfaz completamente traducida al español

### A mejorar
- **Contraste gris/crema:** `#73726C` sobre `#FAF9F5` puede no cumplir WCAG AA (4.5:1) para texto de 12px
- **Botón destructivo sin diferenciación:** "Eliminar cuenta" usa el mismo estilo negro que CTAs positivos
- **Focus visible:** El indicador de focus depende del outline azul del navegador; podría ser más explícito
- **Texto en imágenes:** Los artefactos de inspiración usan imágenes sin alt text descriptivo suficiente

---

## 10. Consistencia del Sistema de Diseño

### Fortalezas
1. **Paleta ultra-cohesiva:** Solo 4 tonos de fondo y 4 de texto en toda la app
2. **Tipografía propia:** `anthropicSans` y `anthropicSerif` crean identidad fuerte
3. **Tono cálido único:** El crema `#FAF9F5` diferencia a Claude de competidores
4. **Componentes uniformes:** Botones, cards e inputs siguen las mismas reglas
5. **Transición light/dark:** Inversión limpia y completa
6. **Empty states cuidados:** Proyectos sin contenido muestra ilustración + CTA

### Inconsistencias detectadas
1. **Border radius variable:** Se usan 6 valores diferentes (6, 8, 10, 12, 16, 9999px); podría reducirse a 4
2. **Font weight 430:** Peso no estándar que podría causar fallback inconsistente en navegadores sin soporte variable fonts
3. **Botones sin padding propio:** Algunos botones ghost tienen `padding: 0px` y dependen del layout padre
4. **Estilo destructivo:** No existe variante de botón de peligro diferenciada visualmente
5. **Sombras azules en upgrade:** La card Pro usa sombras azules que no aparecen en ningún otro lugar de la app

---

## 11. Arquitectura de Tokens de Diseño (3 Niveles)

Claude.ai utiliza un conjunto de design tokens que se pueden estructurar en 3 niveles siguiendo el patrón de sistemas como Material Design 3 (ref/sys/comp), Spectrum de Adobe y Primer de GitHub.

### Tier 1 — Global (Primitivos)

Valores crudos sin contexto semántico. Naming: `--claude-[category]-[value]`.

#### Colores

| Escala | Tokens | Valores |
|--------|--------|---------|
| **Neutral** | 50→900 | #FFFFFF, #FAF9F5, #F0EEE6, #E8E6E0, #A3A29D, #73726C, #3D3D3A, #2A2927, #1F1F1E, #141413 |
| **Beige** | 50→200 | #FAF9F5, #F0EEE6, #E8E6E0 |
| **Blue** | 100→600 | #E3F2FD, #2C84DB, #1B67B2, #1565C0 |
| **Terracotta** | 100→600 | #FAF0EB, #D97757, #C4622D, #A14D23 |
| **Red** | 100→600 | #FFEBEE, #D4432F, #C62828, #8A2424 |
| **Green** | 100, 500 | #E8F5E9, #2E7D32 |
| **Amber** | 100, 500 | #FFF3E0, #E65100 |

#### Espaciado (base 4px)

| Token | Valor |
|-------|-------|
| space-1 → space-16 | 4px, 8px, 12px, 16px, 20px, 24px, 32px, 40px, 48px, 64px |

#### Tipografía

| Categoría | Tokens |
|-----------|--------|
| **Familias** | UI (system sans), Serif (Georgia), Mono (JetBrains), Dyslexia (OpenDyslexic) |
| **Tamaños** | xs: 12px, sm: 14px, md: 16px, lg: 20px, xl: 24px, 2xl: 30px, 3xl: 36px |
| **Pesos** | 400 (regular), 430–500 (medium), 600 (semibold), 700 (bold) |
| **Line-height** | 1.2 (tight), 1.4–1.5 (normal), 1.6 (relaxed) |

#### Otros primitivos

| Categoría | Tokens |
|-----------|--------|
| **Radii** | xs: 4px, sm: 6px, md: 8px, lg: 12px, xl: 16px, full: 9999px |
| **Sombras** | xs: `0 1px 2px rgba(0,0,0,.05)`, sm: `0 2px 8px rgba(0,0,0,.04)`, md: `0 6px 22px rgba(0,0,0,.05)`, accent: `0 4px 24px rgba(27,103,178,.1)` |
| **Bordes** | 1px, 1.5px, 2px · opacidades 0.15, 0.30 |
| **Duración** | 35ms, 100ms, 150ms, 200ms, 300ms |
| **Easing** | standard `cubic-bezier(0.4,0,0.2,1)`, smooth `cubic-bezier(0.65,0,0.35,1)`, ease-out |

### Tier 2 — Semántico (Alias con propósito)

Naming: `--claude-sem-[category]-[role]`. **Solo este tier cambia entre light/dark mode.**

| Categoría | Token | Ref. Global | Valor (light) |
|-----------|-------|-------------|---------------|
| **Background** | sem-bg-page | neutral-100 | #FAF9F5 |
| | sem-bg-surface | neutral-50 | #FFFFFF |
| | sem-bg-inverse | neutral-900 | #141413 |
| | sem-bg-hover | neutral-200 | #F0EEE6 |
| | sem-bg-brand | terracotta-500 | #C4622D |
| | sem-bg-danger | red-400 | #D4432F |
| **Foreground** | sem-fg-primary | neutral-900 | #141413 |
| | sem-fg-secondary | neutral-600 | #3D3D3A |
| | sem-fg-tertiary | neutral-500 | #73726C |
| | sem-fg-link | blue-400 | #2C84DB |
| | sem-fg-danger | red-500 | #C62828 |
| | sem-fg-success | green-500 | #2E7D32 |
| **Border** | sem-border-default | neutral-900 @ .15 | rgba(31,30,29,0.15) |
| | sem-border-strong | neutral-900 @ .30 | rgba(31,30,29,0.30) |
| | sem-border-focus | blue-400 @ .40 | rgba(44,132,219,0.40) |
| **Radius** | sem-radius-card | radius-lg | 12px |
| | sem-radius-button | radius-lg | 12px |
| | sem-radius-pill | radius-full | 9999px |
| **Shadow** | sem-shadow-elevated | shadow-sm | Cards |
| | sem-shadow-floating | shadow-md | Dropdowns, modals |
| | sem-shadow-focus | 0 0 0 3px blue/0.1 | Focus rings |

### Tier 3 — Componente (ejemplo: Button)

Naming: `--claude-comp-btn-[variant]-[property]-[state]`.

| Propiedad | Primary | Secondary | Ghost | Danger |
|-----------|---------|-----------|-------|--------|
| **bg** | #141413 | transparent | transparent | #D4432F |
| **bg-hover** | opacity .85 | #F0EEE6 | #F0EEE6 | opacity .9 |
| **fg** | #FFFFFF | #141413 | #141413 | #FFFFFF |
| **border** | none | rgba(31,30,29,.30) | none | none |
| **radius** | 12px | 12px | 6px | 12px |
| **padding** | 12px 24px | 12px 24px | 8px 12px | 12px 24px |
| **font** | 14px / 500 | 14px / 500 | 14px / 500 | 14px / 500 |

**Cadena de referencia:** `--claude-blue-400` (T1) → `--claude-sem-bg-interactive` (T2) → `--claude-comp-btn-primary-bg` (T3)

> **Dark mode:** Solo los tokens T2 cambian entre themes. T1 permanece constante como paleta base y T3 hereda automáticamente.

---

## 12. Bloques de Código y Syntax Highlighting

### Estilo del contenedor

| Propiedad | Valor |
|-----------|-------|
| **Fuente** | `jetbrains` (custom), fallback: `ui-monospace, SFMono-Regular, Menlo, Monaco` |
| **Tamaño** | `14px` |
| **Line height** | `22.75px` (~1.625) |
| **Padding** | `14px` (3.5 unidades de 4px) |
| **Border radius** | `8px` |
| **Header** | Label de lenguaje ("javascript") + botón "Copiar al portapapeles" |

### Paleta de syntax highlighting

| Color | RGB | Uso |
|-------|-----|-----|
| Base | `rgb(20, 24, 31)` / `#14181F` | Texto base del código |
| Keywords | `rgb(129, 0, 194)` / `#8100C2` | Palabras clave (`function`, `return`) |
| Functions | `rgb(0, 81, 194)` / `#0051C2` | Nombres de funciones |
| Comments | `rgb(43, 48, 59)` / `#2B303B` | Comentarios |
| Numbers | `rgb(184, 79, 5)` / `#B84F05` | Literales numéricos |
| Strings | `rgb(0, 128, 128)` / `#008080` | Cadenas de texto |

### Hallazgos
- El fondo del bloque de código es transparente, hereda del contenedor padre (crema base)
- No hay borde visible, solo el border-radius de 8px
- La paleta de syntax highlighting usa tonos saturados que contrastan bien con el fondo cálido
- El header con label de lenguaje es una buena práctica de UX

---

## 13. Animaciones y Transiciones

### Curvas de easing utilizadas

| Curva | Valor CSS | Uso |
|-------|-----------|-----|
| **Standard** | `cubic-bezier(0.4, 0, 0.2, 1)` | Transiciones generales de UI |
| **Smooth (Quart out)** | `cubic-bezier(0.165, 0.85, 0.45, 1)` | Sidebar, botones, hover states |
| **Ease out** | `cubic-bezier(0, 0, 0.2, 1)` | Opacity fade-in, gap |
| **Ease in** | `cubic-bezier(0.4, 0, 1, 1)` | Opacity fade-out |
| **Spring-like** | `cubic-bezier(0.19, 1, 0.22, 1)` | Transform (apertura de menús) |

### Duraciones

| Duración | Uso |
|----------|-----|
| `35ms` | Micro-interacciones rápidas (bg-color de botones en sidebar) |
| `75ms` | Transiciones ultra-rápidas (hover en items pequeños) |
| `100ms` | Hover en elementos medianos |
| `150ms` | Transiciones estándar (botones, inputs, opacity) |
| `200ms` | Outline focus, transforms |
| `300ms` | Sidebar expand/collapse, hover con múltiples propiedades |
| `500ms` | Fade-out lento de elementos |

### Propiedades animadas

- `background-color` — Hover de botones, sidebar items
- `border-color` — Focus de inputs, hover de bordes
- `box-shadow` — Focus rings, elevación
- `color` — Cambio de color de texto en hover
- `opacity` — Aparición/desaparición de elementos
- `transform` — Apertura de menús, tooltips
- `gap` — Animación de sidebar expand/collapse
- `fill`, `stroke` — Cambio de color en iconos SVG

### Keyframes

| Nombre | Uso |
|--------|-----|
| `ProseMirror-cursor-blink` | Parpadeo del cursor en el editor de texto |
| `look-around` | Micro-animación en el icono de Claude (movimiento sutil) |

### Hallazgos
- **Consistencia:** Se usan 2 curvas principales de easing en toda la app (standard y smooth)
- **Rapidez:** Las duraciones son muy cortas (35–300ms), dando sensación de fluidez inmediata
- **No hay animaciones decorativas excesivas:** Todo es funcional y sutil
- **Sidebar:** La transición de expand/collapse usa `gap 0.3s` con ease-out, creando un efecto suave

---

## 14. Estados de Componentes

### Botones

| Estado | Cambio visual |
|--------|--------------|
| **Default** | Color y fondo base del variante |
| **Hover** | `background-color` cambia (crema `#F0EEE6` para ghost/outline, opacity 0.85 para primario) |
| **Focus** | `outline: 2px` azul del navegador + `box-shadow` sutil |
| **Active/Pressed** | Sin cambio visual adicional visible (sin scale ni darkening) |
| **Disabled** | Opacity reducida, cursor not-allowed |

### Sidebar Items

| Estado | Cambio visual |
|--------|--------------|
| **Default** | Fondo transparente, texto `#3D3D3A` |
| **Hover** | Fondo `#F0EEE6` (crema medio), transición 300ms |
| **Active (selected)** | Fondo `#F0EEE6` + `font-weight: 500` |
| **Focus** | Outline del navegador |

### Inputs

| Estado | Cambio visual |
|--------|--------------|
| **Default** | Borde `rgba(31,30,29,0.3)` |
| **Hover** | Sin cambio visible (no hay hover explícito) |
| **Focus** | Borde `rgba(44,132,219,0.4)` + `box-shadow: 0 0 0 3px rgba(44,132,219,0.1)` |
| **Filled** | Sin cambio respecto a default |
| **Error** | No observado en la auditoría |

### Chat Messages

| Estado | Cambio visual |
|--------|--------------|
| **Default** | Acciones ocultas |
| **Hover** | Aparecen iconos de acción (copiar, like, dislike, retry) con fade-in |
| **Actions hover** | Cada icono tiene hover individual con fondo crema |

### Menú contextual (Dropdown)

| Estado | Cambio visual |
|--------|--------------|
| **Item default** | Fondo transparente |
| **Item hover** | Fondo `#F0EEE6` |
| **Item destructivo** | Texto rojo `#D4432F` ("Eliminar") |
| **Separador** | Línea 1px con `border-light` |

### Modal de confirmación

| Elemento | Estilo |
|----------|--------|
| **Overlay** | Fondo semi-transparente oscuro |
| **Card** | Fondo blanco/crema, `border-radius: 12px`, sombra md |
| **Título** | `font-size: 18px`, `font-weight: 600` |
| **Botón Cancel** | Estilo outline (transparente + borde) |
| **Botón Eliminar** | Fondo rojo `#D4432F`, texto blanco, `border-radius: 8px` |

### Selector de modelo

| Elemento | Estilo |
|----------|--------|
| **Trigger** | Texto + chevron, sin borde visible |
| **Dropdown** | Fondo blanco, sombra md, `border-radius: 12px` |
| **Item seleccionado** | Checkmark azul a la derecha |
| **Item bloqueado (Pro)** | Badge "Actualizar" azul |
| **Separador** | Línea sutil entre secciones |
| **Switch** | Toggle de pensamiento extendido integrado |

### Hallazgos
- **Botón destructivo encontrado:** El modal de eliminar chat SÍ usa botón rojo (`#D4432F`), a diferencia de "Eliminar cuenta" en settings que usa negro. Inconsistencia confirmada.
- **Hover en chat messages:** Las acciones solo aparecen on hover, lo que puede ser un problema de accesibilidad en dispositivos táctiles.
- **Focus visible limitado:** La mayoría de componentes dependen del outline nativo del navegador.

---

## 15. Componentes adicionales descubiertos

### Menú de adjuntos (+ button)

El botón "+" junto al input de chat despliega un menú con:
- **Añadir archivos o fotos** (⌘U) — con icono de clip
- **Hacer una captura de pantalla** — con icono de cámara
- **Añadir al proyecto** — con icono de carpeta + chevron (submenu)
- *Separador*
- **Búsqueda web** — toggle checkbox (activado por defecto, texto azul)
- **Usar estilo** — con chevron (submenu)
- **Añadir conectores** — con icono de puzzle

### Modal de búsqueda (Cmd+K)

- **Trigger:** Link "Buscar" en sidebar o atajo ⌘K
- **Input:** Placeholder "Buscar chats y proyectos", icono de lupa + filtro
- **Resultados:** Lista con icono de chat + título + timestamp relativo ("Última semana")
- **Item activo:** Fondo crema + indicador de Enter (⏎)
- **Overlay:** Fondo semi-transparente

### Dialog promocional (Cowork)

- **Layout:** 2 columnas (texto izquierda, preview derecha)
- **Badge:** "Vista previa" en verde/azul
- **Título:** Serif grande, ~28px
- **CTA primario:** Botón negro "Descargar aplicación de escritorio"
- **CTA secundario:** Botón outline "Más tarde"
- **Botón cerrar:** X en esquina superior derecha

---

## 16. Recomendaciones

1. **Normalizar border-radius:** Reducir de 6 valores a 4 (sm: 6px, md: 8px, lg: 12px, full: 9999px)
2. **Unificar botón destructivo:** El modal de eliminar chat usa rojo `#D4432F`, pero "Eliminar cuenta" en settings usa negro. Unificar a rojo para todas las acciones destructivas.
3. **Mejorar contraste del gris terciario:** Oscurecer `#73726C` a ~`#666` para cumplir WCAG AA en texto pequeño
4. **Documentar font-weight 430:** Si es intencional con variable fonts, tener fallback explícito
5. **Unificar sombras de acento:** Las sombras azules de la card Pro deberían ser parte del sistema o eliminarse
6. **Mejorar alt text de artefactos:** Las imágenes de inspiración necesitan descripciones más detalladas
7. **Focus ring explícito:** Añadir un `outline` o `ring` visible y consistente para navegación por teclado
8. **Acciones de chat en táctil:** Las acciones de mensaje (copiar, like, dislike) solo aparecen en hover. Necesitan alternativa para dispositivos táctiles.
9. **Consistencia de easing:** Se usan 5 curvas de easing diferentes. Considerar reducir a 2-3 (standard, smooth, spring).
10. **Internacionalización del modal de modelo:** Las descripciones de Opus 4.6 están en inglés ("Most capable for ambitious work") mientras el resto de la UI está en español.
11. **Accesibilidad del dialog de búsqueda:** Falta `DialogTitle` accesible (error en consola: "`DialogContent` requires a `DialogTitle`").
