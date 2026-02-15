# Auditoría de Sistema de Diseño — claude.ai

**Fecha:** 12 de febrero de 2026
**Auditor:** Claude (automatizado vía Playwright)
**Versión analizada:** claude.ai (web app, plan gratuito)

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

## 11. Resumen de Tokens de Diseño

```
COLORES
  --color-bg-primary:      #FAF9F5
  --color-bg-secondary:    #F0EEE6
  --color-bg-surface:      #FFFFFF
  --color-bg-inverse:      #141413
  --color-text-primary:    #141413
  --color-text-secondary:  #3D3D3A
  --color-text-tertiary:   #73726C
  --color-text-inverse:    #FFFFFF
  --color-accent:          #2C84DB
  --color-accent-dark:     #1B67B2
  --color-brand:           terracota (icono asterisco)
  --color-border-light:    rgba(31,30,29, 0.15)
  --color-border-medium:   rgba(31,30,29, 0.30)
  --color-border-focus:    rgba(44,132,219, 0.40)

TIPOGRAFÍA
  --font-ui:               anthropicSans
  --font-serif:            anthropicSerif
  --font-mono:             JetBrains Mono
  --font-dyslexia:         OpenDyslexic
  --font-size-xs:          12px
  --font-size-sm:          14px
  --font-size-base:        16px
  --font-size-lg:          20px
  --font-size-xl:          24px
  --font-size-2xl:         30px
  --font-size-3xl:         36-40px

ESPACIADO
  --space-1:  4px
  --space-2:  8px
  --space-3:  10px
  --space-4:  16px
  --space-6:  24px
  --space-8:  32px

RADII
  --radius-sm:    6px
  --radius-md:    8px
  --radius-lg:    12px
  --radius-xl:    16px
  --radius-full:  9999px

SOMBRAS
  --shadow-xs:    0px 1px 2px rgba(0,0,0,0.05)
  --shadow-sm:    0px 2px 8px rgba(0,0,0,0.04)
  --shadow-md:    0px 6px 22px rgba(0,0,0,0.05)
  --shadow-accent: 0px 4px 24px rgba(27,103,178,0.1)
```

---

## 12. Recomendaciones

1. **Normalizar border-radius:** Reducir de 6 valores a 4 (sm: 6px, md: 8px, lg: 12px, full: 9999px)
2. **Añadir botón destructivo:** Crear variante roja/warning para acciones irreversibles
3. **Mejorar contraste del gris terciario:** Oscurecer `#73726C` a ~`#666` para cumplir WCAG AA en texto pequeño
4. **Documentar font-weight 430:** Si es intencional con variable fonts, tener fallback explícito
5. **Unificar sombras de acento:** Las sombras azules de la card Pro deberían ser parte del sistema o eliminarse
6. **Mejorar alt text de artefactos:** Las imágenes de inspiración necesitan descripciones más detalladas
7. **Focus ring explícito:** Añadir un `outline` o `ring` visible y consistente para navegación por teclado
