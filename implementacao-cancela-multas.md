# GUIA DE IMPLEMENTAÇÃO — CANCELA MULTAS
**Studio:** Astroteca Studio | **Cliente:** Paulo Alexandre Souza Pires
**Stack:** Astro 5 + Tailwind v4 (CSS-first) | **Gerado para Claude Code**

---

## PROMPT PARA COLAR NO CLAUDE CODE

```
Você está implementando o site CANCELA MULTAS (Paulo Alexandre Souza Pires).
Siga este documento do início ao fim, passo a passo. Crie cada arquivo exatamente
como especificado. Rode `npm run build` ao final de cada grupo de arquivos e
corrija erros antes de continuar.

Regras absolutas:
- NUNCA hardcode cor, fonte ou tamanho — sempre var(--t-*) ou classes Tailwind
- Sempre <Image /> de astro:assets quando houver imagem real; sem <img> nativo
- Sem `any` no TypeScript, sem `!important` no CSS
- Tema padrão: claro (light). Dark mode via classe .dark no <html>
- Rode npm run build antes de considerar pronto
```

---

## ESTRUTURA DE ARQUIVOS

```
projeto-raiz/
├── astro.config.mjs
├── tsconfig.json
├── .env                               ← Preencher com dados reais
├── src/
│   ├── assets/
│   │   └── (adicionar logo.svg e hero-photo.webp depois)
│   ├── styles/
│   │   ├── tokens.css
│   │   └── global.css
│   ├── layouts/
│   │   └── BaseLayout.astro
│   ├── components/
│   │   ├── ui/
│   │   │   ├── WhatsAppButton.astro
│   │   │   └── DarkModeToggle.astro
│   │   └── sections/
│   │       ├── Header.astro
│   │       ├── Hero.astro
│   │       ├── Servicos.astro
│   │       ├── Diferenciais.astro
│   │       ├── Precos.astro
│   │       ├── Faq.astro
│   │       ├── CtaFinal.astro
│   │       └── Footer.astro
│   └── pages/
│       ├── index.astro
│       ├── politica-de-privacidade.astro
│       └── termos-de-uso.astro
└── public/
    └── favicon.svg
```

---

## PASSO 0 — DEPENDÊNCIAS

Execute no terminal antes de começar:

```bash
npm install tailwindcss @tailwindcss/vite
npm install @fontsource-variable/inter
```

---

## PASSO 1 — `.env`

Crie o arquivo `.env` na raiz do projeto:

```env
# WhatsApp — apenas dígitos, sem símbolos
PUBLIC_WA_NUMBER=5548996729999

# Mensagem pré-preenchida
PUBLIC_WA_MESSAGE=Olá! Vim do Google e gostaria de mais informações

# Google Tag Manager
PUBLIC_GTM_ID=GTM-M7S2PDFR

# Domínio canônico (sem barra final)
PUBLIC_SITE_URL=https://cancelamulta.com.br
```

---

## PASSO 2 — `astro.config.mjs`

Sobrescreva (ou crie) o arquivo de configuração:

```js
import { defineConfig } from 'astro/config';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
  site: process.env.PUBLIC_SITE_URL ?? 'https://cancelamulta.com.br',
  vite: {
    plugins: [tailwindcss()],
  },
});
```

---

## PASSO 3 — `src/styles/tokens.css`

```css
/* =============================================
   TOKENS — CANCELA MULTAS
   NUNCA edite os nomes, apenas os valores.
   ============================================= */

:root {
  /* Cores de marca */
  --t-primary:      #144e74;
  --t-primary-dark: #0f3e5e;
  --t-secondary:    #edbd24;

  /* Superfícies (tema claro) */
  --t-background:   #fcfcfc;
  --t-surface:      #fafafa;
  --t-surface-alt:  #f0f4f7;
  --t-dark:         #1a1a1a;

  /* Tipografia (tema claro) */
  --t-text-main:    #333333;
  --t-text-soft:    #595959;
  --t-text-muted:   #808080;

  /* Bordas (tema claro) */
  --t-border:       #d8d8d8;

  /* Famílias tipográficas */
  --t-font-serif: 'Inter Variable', 'Inter', sans-serif;
  --t-font-sans:  'Inter Variable', 'Inter', sans-serif;
}

/* ── Dark mode ───────────────────────────── */
.dark {
  --t-background:  #121212;
  --t-surface:     #212121;
  --t-surface-alt: #303030;
  --t-text-main:   #e6e6e6;
  --t-text-soft:   #b3b3b3;
  --t-text-muted:  #737373;
  --t-border:      #333333;
}
```

---

## PASSO 4 — `src/styles/global.css`

```css
/* ── Fontes ──────────────────────────────── */
@import "@fontsource-variable/inter";

/* ── Tailwind v4 (CSS-first) ─────────────── */
@import "tailwindcss";

/* ── Tokens ──────────────────────────────── */
@import "./tokens.css";

/* ── Dark mode via classe .dark no <html> ── */
@custom-variant dark (&:where(.dark, .dark *));

/* ── Tema Tailwind: mapeia tokens → classes ─ */
@theme {
  /* Fontes */
  --font-serif: var(--t-font-serif);
  --font-sans:  var(--t-font-sans);

  /* Cores (habilita bg-primary, text-primary, etc.) */
  --color-primary:      var(--t-primary);
  --color-primary-dark: var(--t-primary-dark);
  --color-secondary:    var(--t-secondary);
  --color-background:   var(--t-background);
  --color-surface:      var(--t-surface);
  --color-surface-alt:  var(--t-surface-alt);
  --color-dark:         var(--t-dark);
  --color-text-main:    var(--t-text-main);
  --color-text-soft:    var(--t-text-soft);
  --color-text-muted:   var(--t-text-muted);
  --color-border:       var(--t-border);
}

/* ── Utilitários de layout ───────────────── */
@utility section-py {
  padding-top: 4.5rem;
  padding-bottom: 4.5rem;

  @media (min-width: 768px) {
    padding-top: 6rem;
    padding-bottom: 6rem;
  }
}

@utility container-wide {
  width: 100%;
  max-width: 1280px;
  margin-inline: auto;
  padding-inline: 1.25rem;

  @media (min-width: 640px) {
    padding-inline: 1.5rem;
  }
}

@utility container-content {
  width: 100%;
  max-width: 760px;
  margin-inline: auto;
  padding-inline: 1.25rem;

  @media (min-width: 640px) {
    padding-inline: 1.5rem;
  }
}

/* ── Utilitários tipográficos ─────────────── */
@utility text-display-md {
  font-size: clamp(2rem, 5vw, 3.25rem);
  line-height: 1.1;
  font-weight: 800;
  letter-spacing: -0.02em;
}

@utility text-display-sm {
  font-size: clamp(1.5rem, 3.5vw, 2.25rem);
  line-height: 1.2;
  font-weight: 700;
  letter-spacing: -0.015em;
}

@utility text-body-lg {
  font-size: clamp(1rem, 2vw, 1.125rem);
  line-height: 1.75;
}

@utility text-text-main {
  color: var(--t-text-main);
}

@utility text-text-soft {
  color: var(--t-text-soft);
}

@utility text-text-muted {
  color: var(--t-text-muted);
}

/* ── Base global ─────────────────────────── */
html {
  scroll-behavior: smooth;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  background-color: var(--t-background);
  color: var(--t-text-main);
  font-family: var(--t-font-sans);
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

/* Acessibilidade: foco visível */
:focus-visible {
  outline: 3px solid var(--t-secondary);
  outline-offset: 3px;
  border-radius: 4px;
}
```

---

## PASSO 5 — `src/layouts/BaseLayout.astro`

```astro
---
import '../styles/global.css';
import WhatsAppButton from '../components/ui/WhatsAppButton.astro';

interface Props {
  title?: string;
  description?: string;
  canonical?: string;
  ogImage?: string;
  schema?: Record<string, unknown>;
}

const {
  title = 'Cancela Multas | Recursos de Trânsito e Defesa da CNH Online',
  description = 'Especialistas em recursos de multas de trânsito e defesa da CNH em todo o Brasil. Proteja sua carteira contra suspensão e cassação com agilidade, transparência e análise técnica detalhada. Análise inicial gratuita!',
  ogImage = '/og-image.jpg',
} = Astro.props;

const siteUrl = import.meta.env.PUBLIC_SITE_URL ?? 'https://cancelamulta.com.br';
const canonical = Astro.props.canonical ?? siteUrl;
const gtmId = import.meta.env.PUBLIC_GTM_ID;

/* ── Schema.org — LocalBusiness ──────────── */
const defaultSchema: Record<string, unknown> = {
  '@context': 'https://schema.org',
  '@type': 'LocalBusiness',
  name: 'Cancela Multas',
  description:
    'Especialistas em recursos de multas de trânsito e defesa da CNH em todo o Brasil.',
  url: siteUrl,
  telephone: '+5548996729999',
  priceRange: 'R$40 - R$120',
  areaServed: {
    '@type': 'Country',
    name: 'Brazil',
  },
  openingHoursSpecification: {
    '@type': 'OpeningHoursSpecification',
    dayOfWeek: [
      'Monday', 'Tuesday', 'Wednesday',
      'Thursday', 'Friday', 'Saturday',
    ],
    opens: '08:00',
    closes: '18:00',
  },
  serviceType: 'Recursos Administrativos de Multas de Trânsito',
  sameAs: [],
};

const finalSchema = Astro.props.schema ?? defaultSchema;
---

<!doctype html>
<html lang="pt-BR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="theme-color" content="#144e74" />

    <!-- SEO primário -->
    <title>{title}</title>
    <meta name="description" content={description} />
    <link rel="canonical" href={canonical} />
    <meta
      name="keywords"
      content="recurso multa, cancelar multa, defesa CNH, lei seca, suspensão CNH, cassação CNH, direito de trânsito, multa de trânsito, processo administrativo multa"
    />
    <meta name="robots" content="index, follow" />
    <meta name="author" content="Cancela Multas" />

    <!-- Open Graph -->
    <meta property="og:type" content="website" />
    <meta property="og:url" content={canonical} />
    <meta property="og:title" content={title} />
    <meta property="og:description" content={description} />
    <meta property="og:image" content={ogImage} />
    <meta property="og:locale" content="pt_BR" />
    <meta property="og:site_name" content="Cancela Multas" />

    <!-- Twitter Card -->
    <meta name="twitter:card" content="summary_large_image" />
    <meta name="twitter:title" content={title} />
    <meta name="twitter:description" content={description} />
    <meta name="twitter:image" content={ogImage} />

    <!-- Fonte: Inter via Google Fonts (preconnect + fallback CDN) -->
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&display=swap"
      rel="stylesheet"
    />

    <!-- Schema.org JSON-LD -->
    <script type="application/ld+json" set:html={JSON.stringify(finalSchema)} />

    <!-- Google Tag Manager -->
    {
      gtmId && (
        <script is:inline define:vars={{ gtmId }}>
          (function (w, d, s, l, i) {
            w[l] = w[l] || [];
            w[l].push({ 'gtm.start': new Date().getTime(), event: 'gtm.js' });
            var f = d.getElementsByTagName(s)[0],
              j = d.createElement(s),
              dl = l != 'dataLayer' ? '&l=' + l : '';
            j.async = true;
            j.src =
              'https://www.googletagmanager.com/gtm.js?id=' + i + dl;
            f.parentNode.insertBefore(j, f);
          })(window, document, 'script', 'dataLayer', gtmId);
        </script>
      )
    }

    <!-- Dark mode: previne flash na primeira carga -->
    <script is:inline>
      (function () {
        try {
          const stored = localStorage.getItem('theme');
          if (stored === 'dark') {
            document.documentElement.classList.add('dark');
          }
        } catch (_) {}
      })();
    </script>
  </head>

  <body>
    <!-- GTM noscript -->
    {
      gtmId && (
        <noscript>
          <iframe
            src={`https://www.googletagmanager.com/ns.html?id=${gtmId}`}
            height="0"
            width="0"
            style="display:none;visibility:hidden"
          />
        </noscript>
      )
    }

    <slot />

    <WhatsAppButton />
  </body>
</html>
```

---

## PASSO 6 — COMPONENTES UI

### `src/components/ui/WhatsAppButton.astro`

```astro
---
const waNumber = import.meta.env.PUBLIC_WA_NUMBER ?? '';
const waMessage = import.meta.env.PUBLIC_WA_MESSAGE ?? '';
const waUrl = `https://wa.me/${waNumber}?text=${encodeURIComponent(waMessage)}`;
---

<a
  id="wa-float"
  href={waUrl}
  target="_blank"
  rel="noopener noreferrer"
  aria-label="Falar no WhatsApp"
  class="fixed bottom-6 right-6 z-50 flex items-center justify-center w-14 h-14 rounded-full shadow-xl transition-all duration-300"
  style="background-color: #25D366; color: white;"
>
  <!-- Ícone WhatsApp -->
  <svg
    width="28"
    height="28"
    viewBox="0 0 24 24"
    fill="currentColor"
    aria-hidden="true"
  >
    <path
      d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 0 1-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 0 1-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 0 1 2.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0 0 12.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 0 0 5.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 0 0-3.48-8.413z"
    />
  </svg>
</a>

<script>
  const waBtn = document.getElementById('wa-float');
  const hero = document.getElementById('hero-section');
  const footer = document.getElementById('footer');

  if (waBtn) {
    const observer = new IntersectionObserver(
      (entries) => {
        let anyVisible = false;
        entries.forEach((e) => {
          if (e.isIntersecting) anyVisible = true;
        });
        waBtn.style.opacity = anyVisible ? '0' : '1';
        waBtn.style.pointerEvents = anyVisible ? 'none' : 'auto';
        waBtn.style.transform = anyVisible ? 'scale(0.8)' : 'scale(1)';
      },
      { threshold: 0.15 }
    );

    if (hero) observer.observe(hero);
    if (footer) observer.observe(footer);
  }
</script>
```

---

### `src/components/ui/DarkModeToggle.astro`

```astro
<button
  id="dark-toggle"
  aria-label="Alternar tema escuro/claro"
  class="flex items-center justify-center w-10 h-10 rounded-full transition-all duration-200 cursor-pointer"
  style="background-color: rgba(255,255,255,0.12); color: rgba(255,255,255,0.8);"
>
  <!-- Lua (visível no tema claro) -->
  <svg
    id="icon-moon"
    width="18"
    height="18"
    viewBox="0 0 24 24"
    fill="none"
    stroke="currentColor"
    stroke-width="2"
    stroke-linecap="round"
    stroke-linejoin="round"
    aria-hidden="true"
  >
    <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z" />
  </svg>

  <!-- Sol (visível no tema escuro) -->
  <svg
    id="icon-sun"
    width="18"
    height="18"
    viewBox="0 0 24 24"
    fill="none"
    stroke="currentColor"
    stroke-width="2"
    stroke-linecap="round"
    stroke-linejoin="round"
    class="hidden"
    aria-hidden="true"
  >
    <circle cx="12" cy="12" r="5" />
    <line x1="12" y1="1" x2="12" y2="3" />
    <line x1="12" y1="21" x2="12" y2="23" />
    <line x1="4.22" y1="4.22" x2="5.64" y2="5.64" />
    <line x1="18.36" y1="18.36" x2="19.78" y2="19.78" />
    <line x1="1" y1="12" x2="3" y2="12" />
    <line x1="21" y1="12" x2="23" y2="12" />
    <line x1="4.22" y1="19.78" x2="5.64" y2="18.36" />
    <line x1="18.36" y1="5.64" x2="19.78" y2="4.22" />
  </svg>
</button>

<script>
  const toggle = document.getElementById('dark-toggle');
  const iconSun = document.getElementById('icon-sun');
  const iconMoon = document.getElementById('icon-moon');
  const html = document.documentElement;

  function syncIcons() {
    const isDark = html.classList.contains('dark');
    iconSun?.classList.toggle('hidden', !isDark);
    iconMoon?.classList.toggle('hidden', isDark);
  }

  syncIcons();

  toggle?.addEventListener('click', () => {
    html.classList.toggle('dark');
    try {
      localStorage.setItem(
        'theme',
        html.classList.contains('dark') ? 'dark' : 'light'
      );
    } catch (_) {}
    syncIcons();
  });
</script>
```

---

## PASSO 7 — SEÇÕES

### `src/components/sections/Header.astro`

```astro
---
const waNumber = import.meta.env.PUBLIC_WA_NUMBER ?? '';
const waMessage = import.meta.env.PUBLIC_WA_MESSAGE ?? '';
const waUrl = `https://wa.me/${waNumber}?text=${encodeURIComponent(waMessage)}`;
---

<header
  id="site-header"
  class="fixed top-0 left-0 right-0 z-40 transition-all duration-300"
  style="background-color: var(--t-background); border-bottom: 1px solid var(--t-border);"
>
  <div class="container-wide flex items-center justify-between h-16 md:h-20">

    <!-- Logo -->
    <a
      href="/"
      aria-label="Cancela Multas — Página inicial"
      class="flex items-center gap-1 flex-shrink-0"
    >
      <span
        class="font-serif font-black text-xl md:text-2xl tracking-tight select-none"
        style="color: var(--t-primary);"
      >
        CANCELA
      </span>
      <span
        class="font-serif font-black text-xl md:text-2xl tracking-tight select-none"
        style="color: var(--t-secondary);"
      >
        MULTAS
      </span>
    </a>

    <!-- Centro: horário (desktop) -->
    <div
      class="hidden md:flex items-center gap-2 text-sm font-medium"
      style="color: var(--t-text-soft);"
    >
      <svg
        width="16"
        height="16"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round"
        aria-hidden="true"
      >
        <circle cx="12" cy="12" r="10" />
        <polyline points="12 6 12 12 16 14" />
      </svg>
      <span>Atendimento: Seg a Sáb</span>
    </div>

    <!-- CTA WhatsApp -->
    <a
      href={waUrl}
      target="_blank"
      rel="noopener noreferrer"
      class="flex items-center gap-2 rounded-full px-4 py-2.5 md:px-6 md:py-3 text-sm font-bold text-white transition-all duration-200 hover:opacity-90 active:scale-95 flex-shrink-0"
      style="background-color: var(--t-primary);"
    >
      <!-- Ícone WhatsApp mini -->
      <svg
        width="16"
        height="16"
        viewBox="0 0 24 24"
        fill="currentColor"
        aria-hidden="true"
        class="flex-shrink-0"
      >
        <path
          d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 0 1-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 0 1-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 0 1 2.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0 0 12.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 0 0 5.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 0 0-3.48-8.413z"
        />
      </svg>
      <span class="hidden sm:inline">Falar no WhatsApp</span>
      <span class="sm:hidden">WhatsApp</span>
    </a>
  </div>
</header>

<!-- Espaçador para header fixo -->
<div class="h-16 md:h-20" aria-hidden="true"></div>

<script>
  const header = document.getElementById('site-header');
  let lastY = 0;
  let ticking = false;

  function onScroll() {
    const y = window.scrollY;
    if (!header) return;

    if (y > 80) {
      header.style.boxShadow = '0 2px 20px rgba(0,0,0,0.1)';
      if (y > lastY) {
        header.style.transform = 'translateY(-100%)';
      } else {
        header.style.transform = 'translateY(0)';
      }
    } else {
      header.style.boxShadow = 'none';
      header.style.transform = 'translateY(0)';
    }

    lastY = y;
    ticking = false;
  }

  window.addEventListener(
    'scroll',
    () => {
      if (!ticking) {
        requestAnimationFrame(onScroll);
        ticking = true;
      }
    },
    { passive: true }
  );
</script>
```

---

### `src/components/sections/Hero.astro`

```astro
---
const waNumber = import.meta.env.PUBLIC_WA_NUMBER ?? '';
const waMessage = import.meta.env.PUBLIC_WA_MESSAGE ?? '';
const waUrl = `https://wa.me/${waNumber}?text=${encodeURIComponent(waMessage)}`;

const benefits = [
  'Atendimento rápido pelo WhatsApp, sem burocracia',
  'Recurso para multas médias, graves, gravíssimas e processos suspensivos',
  'Análise gratuita antes de qualquer pagamento',
];
---

<section
  id="hero-section"
  class="relative overflow-hidden"
  style="background-color: var(--t-primary); min-height: 580px;"
>
  <!-- Decorações geométricas de fundo -->
  <div class="absolute inset-0 pointer-events-none overflow-hidden" aria-hidden="true">
    <!-- Círculo grande direito superior -->
    <div
      class="absolute rounded-full"
      style="
        width: 480px; height: 480px;
        top: -120px; right: -120px;
        background-color: var(--t-secondary);
        opacity: 0.08;
      "
    ></div>
    <!-- Círculo médio esquerdo inferior -->
    <div
      class="absolute rounded-full"
      style="
        width: 200px; height: 200px;
        bottom: -60px; left: -40px;
        background-color: var(--t-secondary);
        opacity: 0.1;
      "
    ></div>
    <!-- Retângulo inclinado -->
    <div
      class="absolute rotate-12"
      style="
        width: 60px; height: 200px;
        top: 40%; right: 15%;
        background-color: rgba(255,255,255,0.04);
        border-radius: 12px;
      "
    ></div>
  </div>

  <div class="container-wide section-py relative">
    <div class="grid md:grid-cols-2 gap-10 lg:gap-16 items-center">

      <!-- ── Coluna esquerda: Copy ── -->
      <div>
        <!-- Badge -->
        <div
          class="inline-flex items-center gap-2 rounded-full px-4 py-1.5 text-sm font-bold mb-6"
          style="background-color: var(--t-secondary); color: var(--t-dark);"
        >
          <svg
            width="13"
            height="13"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="3"
            stroke-linecap="round"
            stroke-linejoin="round"
            aria-hidden="true"
          >
            <polyline points="20 6 9 17 4 12" />
          </svg>
          Análise Inicial Gratuita
        </div>

        <!-- Título H1 -->
        <h1
          class="font-serif text-display-md text-white mb-5"
        >
          Levou Multa ou sua CNH Pode ser Suspensa?
          <span style="color: var(--t-secondary);"> A Gente Resolve.</span>
        </h1>

        <!-- Subtítulo -->
        <p
          class="text-body-lg mb-8"
          style="color: rgba(255,255,255,0.80);"
        >
          Somos especialistas em recursos administrativos de trânsito. Analisamos
          seu caso gratuitamente e aplicamos a estratégia certa para proteger sua
          carteira de motorista. Atendimento 100% online em todo o Brasil.
        </p>

        <!-- CTAs -->
        <div class="flex flex-col sm:flex-row gap-3 mb-10">
          <!-- CTA primário -->
          <a
            href={waUrl}
            target="_blank"
            rel="noopener noreferrer"
            class="flex items-center justify-center gap-2 rounded-xl px-6 py-4 font-bold text-base transition-all duration-200 hover:opacity-90 active:scale-[0.97]"
            style="background-color: var(--t-secondary); color: var(--t-dark); min-height: 52px;"
          >
            <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
              <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 0 1-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 0 1-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 0 1 2.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0 0 12.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 0 0 5.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 0 0-3.48-8.413z"/>
            </svg>
            Analisar Minha Multa Agora
          </a>

          <!-- CTA secundário -->
          <a
            href={waUrl}
            target="_blank"
            rel="noopener noreferrer"
            class="flex items-center justify-center gap-2 rounded-xl px-6 py-4 font-semibold text-base transition-all duration-200 hover:bg-white/10"
            style="border: 2px solid rgba(255,255,255,0.35); color: white; min-height: 52px;"
          >
            Falar com um Especialista
          </a>
        </div>

        <!-- Lista de benefícios -->
        <ul class="flex flex-col gap-3 list-none p-0 m-0">
          {benefits.map((b) => (
            <li class="flex items-start gap-3">
              <span
                class="flex-shrink-0 flex items-center justify-center w-5 h-5 rounded-full mt-0.5"
                style="background-color: var(--t-secondary);"
                aria-hidden="true"
              >
                <svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3.5" stroke-linecap="round" stroke-linejoin="round" style="color: var(--t-dark);">
                  <polyline points="20 6 9 17 4 12"/>
                </svg>
              </span>
              <span class="text-sm leading-relaxed" style="color: rgba(255,255,255,0.82);">{b}</span>
            </li>
          ))}
        </ul>
      </div>

      <!-- ── Coluna direita: Card de estatísticas ── -->
      <div class="hidden md:flex justify-center items-center">
        <div class="relative w-full max-w-xs">
          <!-- Card principal -->
          <div
            class="rounded-2xl p-7 w-full"
            style="
              background-color: rgba(255,255,255,0.07);
              border: 1px solid rgba(255,255,255,0.13);
              backdrop-filter: blur(8px);
            "
          >
            <!-- Stat 1 -->
            <div
              class="flex items-center gap-4 pb-5 mb-5"
              style="border-bottom: 1px solid rgba(255,255,255,0.1);"
            >
              <div
                class="flex-shrink-0 w-12 h-12 rounded-xl flex items-center justify-center"
                style="background-color: var(--t-secondary);"
                aria-hidden="true"
              >
                <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="color: var(--t-dark);">
                  <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/>
                  <polyline points="14 2 14 8 20 8"/>
                  <line x1="16" y1="13" x2="8" y2="13"/>
                  <line x1="16" y1="17" x2="8" y2="17"/>
                </svg>
              </div>
              <div>
                <p class="text-2xl font-black text-white leading-none mb-1">+1.000</p>
                <p class="text-xs" style="color: rgba(255,255,255,0.6);">recursos analisados</p>
              </div>
            </div>

            <!-- Stat 2 -->
            <div
              class="flex items-center gap-4 pb-5 mb-5"
              style="border-bottom: 1px solid rgba(255,255,255,0.1);"
            >
              <div
                class="flex-shrink-0 w-12 h-12 rounded-xl flex items-center justify-center"
                style="background-color: rgba(255,255,255,0.12);"
                aria-hidden="true"
              >
                <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="color: white;">
                  <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/>
                </svg>
              </div>
              <div>
                <p class="text-2xl font-black text-white leading-none mb-1">CNH</p>
                <p class="text-xs" style="color: rgba(255,255,255,0.6);">protegida em todo o Brasil</p>
              </div>
            </div>

            <!-- Stat 3 -->
            <div class="flex items-center gap-4">
              <div
                class="flex-shrink-0 w-12 h-12 rounded-xl flex items-center justify-center"
                style="background-color: rgba(255,255,255,0.12);"
                aria-hidden="true"
              >
                <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="color: white;">
                  <rect x="2" y="3" width="20" height="14" rx="2" ry="2"/>
                  <line x1="8" y1="21" x2="16" y2="21"/>
                  <line x1="12" y1="17" x2="12" y2="21"/>
                </svg>
              </div>
              <div>
                <p class="text-2xl font-black text-white leading-none mb-1">100%</p>
                <p class="text-xs" style="color: rgba(255,255,255,0.6);">atendimento online</p>
              </div>
            </div>
          </div>

          <!-- Acento flutuante superior direito -->
          <div
            class="absolute -top-4 -right-4 w-14 h-14 rounded-2xl rotate-12"
            style="background-color: var(--t-secondary); opacity: 0.85;"
            aria-hidden="true"
          ></div>
          <!-- Acento flutuante inferior esquerdo -->
          <div
            class="absolute -bottom-3 -left-3 w-9 h-9 rounded-xl -rotate-6"
            style="background-color: rgba(255,255,255,0.14);"
            aria-hidden="true"
          ></div>
        </div>
      </div>
    </div>
  </div>
</section>
```

---

### `src/components/sections/Servicos.astro`

```astro
---
const waNumber = import.meta.env.PUBLIC_WA_NUMBER ?? '';
const waMessage = import.meta.env.PUBLIC_WA_MESSAGE ?? '';
const waUrl = `https://wa.me/${waNumber}?text=${encodeURIComponent(waMessage)}`;

interface Servico {
  icon: string;          // SVG path(s) string
  viewBox: string;
  nome: string;
  descricao: string;
  precos?: { label: string; valor: string }[];
  ctaTexto: string;
  destaque?: boolean;
}

const servicos: Servico[] = [
  {
    viewBox: '0 0 24 24',
    icon: '<path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="16" y1="13" x2="8" y2="13"/><line x1="16" y1="17" x2="8" y2="17"/>',
    nome: 'Recurso sem Efeito Suspensivo',
    descricao:
      'Para infrações médias, graves e gravíssimas que ainda não afetam sua CNH imediatamente. Analisamos a multa, identificamos erros técnicos e entramos com o recurso mais adequado para reduzir ou cancelar a penalidade.',
    precos: [
      { label: 'Média', valor: 'R$ 40' },
      { label: 'Grave', valor: 'R$ 80' },
      { label: 'Gravíssima', valor: 'R$ 120' },
    ],
    ctaTexto: 'Quero Recorrer desta Multa',
  },
  {
    viewBox: '0 0 24 24',
    icon: '<path d="M10.29 3.86L1.82 18a2 2 0 0 0 1.71 3h16.94a2 2 0 0 0 1.71-3L13.71 3.86a2 2 0 0 0-3.42 0z"/><line x1="12" y1="9" x2="12" y2="13"/><line x1="12" y1="17" x2="12.01" y2="17"/>',
    nome: 'Recurso com Efeito Suspensivo',
    descricao:
      'Alguns tipos de infração suspendem a CNH assim que são aplicadas. Se você recebeu uma multa gravíssima com efeito suspensivo, precisa agir rápido. Analisamos seu caso e buscamos reverter a suspensão antes que entre em vigor.',
    ctaTexto: 'Analisar Minha Situação Agora',
    destaque: true,
  },
  {
    viewBox: '0 0 24 24',
    icon: '<path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/>',
    nome: 'Suspensão e Cassação da CNH (PSDD e PCDD)',
    descricao:
      'Se você acumulou pontos demais ou está respondendo a um processo de suspensão ou cassação, ainda há como se defender. Montamos a estratégia adequada para cada etapa e acompanhamos até a decisão final.',
    ctaTexto: 'Quero Defender Minha CNH',
  },
  {
    viewBox: '0 0 24 24',
    icon: '<path d="M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.77-3.77a6 6 0 0 1-7.94 7.94l-6.91 6.91a2.12 2.12 0 0 1-3-3l6.91-6.91a6 6 0 0 1 7.94-7.94l-3.76 3.76z"/>',
    nome: 'Outros Processos de Trânsito',
    descricao:
      'Atuamos também em multas na CNH provisória, casos de Lei Seca, ação de indicação de condutor e outros processos administrativos de trânsito. Fale com a gente para analisar o seu caso específico.',
    ctaTexto: 'Falar sobre Meu Caso',
  },
];
---

<section
  id="servicos"
  class="section-py"
  style="background-color: var(--t-surface-alt);"
>
  <div class="container-wide">
    <!-- Cabeçalho -->
    <div class="text-center mb-12 container-content mx-auto">
      <h2
        class="font-serif text-display-sm mb-4"
        style="color: var(--t-text-main);"
      >
        Qual é a Sua Situação?
      </h2>
      <p class="text-body-lg" style="color: var(--t-text-soft);">
        Atendemos desde multas comuns até processos de suspensão e cassação da
        CNH. Veja qual serviço se encaixa no seu caso.
      </p>
    </div>

    <!-- Grid de serviços -->
    <div class="grid sm:grid-cols-2 gap-6">
      {servicos.map((s) => (
        <article
          class="rounded-2xl p-7 flex flex-col transition-shadow duration-200 hover:shadow-lg"
          style={`
            background-color: var(--t-surface);
            border: 2px solid ${s.destaque ? 'var(--t-primary)' : 'var(--t-border)'};
            position: relative;
            overflow: hidden;
          `}
        >
          {/* Acento superior para o card em destaque */}
          {s.destaque && (
            <div
              class="absolute top-0 left-0 right-0 h-1"
              style="background-color: var(--t-primary);"
              aria-hidden="true"
            />
          )}

          {/* Ícone */}
          <div
            class="w-12 h-12 rounded-xl flex items-center justify-center mb-5 flex-shrink-0"
            style={`background-color: ${s.destaque ? 'var(--t-primary)' : 'var(--t-surface-alt)'};`}
            aria-hidden="true"
          >
            <svg
              width="22"
              height="22"
              viewBox={s.viewBox}
              fill="none"
              stroke={s.destaque ? 'white' : 'var(--t-primary)'}
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
              set:html={s.icon}
            />
          </div>

          {/* Nome */}
          <h3
            class="font-serif font-bold text-lg mb-3"
            style="color: var(--t-text-main);"
          >
            {s.nome}
          </h3>

          {/* Descrição */}
          <p class="text-sm leading-relaxed mb-5 flex-1" style="color: var(--t-text-soft);">
            {s.descricao}
          </p>

          {/* Preços (apenas serviço 1) */}
          {s.precos && (
            <div class="flex flex-wrap gap-2 mb-5">
              {s.precos.map((p) => (
                <span
                  class="inline-flex items-center gap-1.5 rounded-full px-3 py-1 text-xs font-semibold"
                  style="background-color: var(--t-surface-alt); color: var(--t-text-main);"
                >
                  <span style="color: var(--t-text-muted);">{p.label}:</span>
                  <strong style="color: var(--t-primary);">{p.valor}</strong>
                </span>
              ))}
            </div>
          )}

          {/* CTA */}
          <a
            href={waUrl}
            target="_blank"
            rel="noopener noreferrer"
            class="flex items-center justify-center gap-2 rounded-xl px-5 py-3.5 text-sm font-bold transition-all duration-200 hover:opacity-90 active:scale-[0.97] mt-auto"
            style={`
              background-color: ${s.destaque ? 'var(--t-primary)' : 'transparent'};
              color: ${s.destaque ? 'white' : 'var(--t-primary)'};
              border: 2px solid var(--t-primary);
              min-height: 44px;
            `}
          >
            {s.ctaTexto}
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
              <polyline points="9 18 15 12 9 6"/>
            </svg>
          </a>
        </article>
      ))}
    </div>
  </div>
</section>
```

---

### `src/components/sections/Diferenciais.astro`

```astro
---
interface Diferencial {
  viewBox: string;
  icon: string;
  titulo: string;
  descricao: string;
}

const diferenciais: Diferencial[] = [
  {
    viewBox: '0 0 24 24',
    icon: '<circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/>',
    titulo: 'Análise Técnica Detalhada Antes do Recurso',
    descricao:
      'Estudamos cada detalhe da sua multa antes de qualquer ação: erros técnicos, falhas no auto de infração e argumentos que aumentam as chances de sucesso.',
  },
  {
    viewBox: '0 0 24 24',
    icon: '<path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/><circle cx="12" cy="12" r="3"/>',
    titulo: 'Transparência Total sobre as Chances Reais',
    descricao:
      'Você sabe exatamente o que pode esperar antes de pagar qualquer coisa. Sem promessas que não podemos cumprir e sem surpresas no meio do processo.',
  },
  {
    viewBox: '0 0 24 24',
    icon: '<circle cx="12" cy="8" r="7"/><polyline points="8.21 13.89 7 23 12 20 17 23 15.79 13.88"/>',
    titulo: 'Especialistas em Suspensão, Cassação e Lei Seca',
    descricao:
      'Além dos recursos comuns, atuamos em casos graves que exigem conhecimento específico e resposta rápida. São situações em que a escolha do especialista faz toda a diferença.',
  },
  {
    viewBox: '0 0 24 24',
    icon: '<circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/>',
    titulo: 'Acompanhamento Completo até a Decisão Final',
    descricao:
      'Cuidamos de prazos, documentos e todas as etapas do processo. Você não fica sem resposta e não precisa correr atrás de nada sozinho.',
  },
  {
    viewBox: '0 0 24 24',
    icon: '<path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>',
    titulo: 'Linguagem Simples, sem Juridiquês',
    descricao:
      'Explicamos tudo de forma clara e direta. Você entende o que está acontecendo no seu caso sem precisar decifrar termos técnicos.',
  },
  {
    viewBox: '0 0 24 24',
    icon: '<circle cx="12" cy="12" r="10"/><line x1="2" y1="12" x2="22" y2="12"/><path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/>',
    titulo: 'Atendimento Online em Todo o Brasil',
    descricao:
      'Motoristas de qualquer estado são atendidos pelo WhatsApp. Toda a documentação é processada de forma digital, com segurança e agilidade.',
  },
];
---

<section
  id="diferenciais"
  class="section-py"
  style="background-color: var(--t-background);"
>
  <div class="container-wide">
    <!-- Cabeçalho -->
    <div class="text-center mb-12 container-content mx-auto">
      <h2
        class="font-serif text-display-sm mb-4"
        style="color: var(--t-text-main);"
      >
        Por que Confiar na Cancela Multas?
      </h2>
      <p class="text-body-lg" style="color: var(--t-text-soft);">
        Não somos um escritório genérico. Somos especialistas em trânsito com
        foco em resultado real e transparência total em cada caso.
      </p>
    </div>

    <!-- Grid 3×2 -->
    <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6">
      {diferenciais.map((d, i) => (
        <article
          class="rounded-2xl p-6 flex flex-col gap-4 transition-shadow duration-200 hover:shadow-md"
          style="background-color: var(--t-surface); border: 1px solid var(--t-border);"
        >
          {/* Ícone com número de ordem em sobreposição sutil */}
          <div class="flex items-start gap-4">
            <div
              class="flex-shrink-0 w-11 h-11 rounded-xl flex items-center justify-center"
              style="background-color: var(--t-primary); color: white;"
              aria-hidden="true"
            >
              <svg
                width="20"
                height="20"
                viewBox={d.viewBox}
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
                set:html={d.icon}
              />
            </div>

            <div class="flex-1">
              <h3
                class="font-serif font-bold text-base leading-snug"
                style="color: var(--t-text-main);"
              >
                {d.titulo}
              </h3>
            </div>
          </div>

          <p class="text-sm leading-relaxed" style="color: var(--t-text-soft);">
            {d.descricao}
          </p>
        </article>
      ))}
    </div>
  </div>
</section>
```

---

### `src/components/sections/Precos.astro`

```astro
---
const waNumber = import.meta.env.PUBLIC_WA_NUMBER ?? '';
const waMessage = import.meta.env.PUBLIC_WA_MESSAGE ?? '';
const waUrl = `https://wa.me/${waNumber}?text=${encodeURIComponent(waMessage)}`;

interface Plano {
  nome: string;
  preco: string;
  descricao: string;
  ctaTexto: string;
  destaque?: boolean;
  badge?: string;
}

const planos: Plano[] = [
  {
    nome: 'Infração Média',
    preco: 'R$ 40,00',
    descricao: 'Recurso administrativo para infrações de natureza média.',
    ctaTexto: 'Quero Recorrer',
  },
  {
    nome: 'Infração Grave',
    preco: 'R$ 80,00',
    descricao: 'Recurso administrativo para infrações de natureza grave.',
    ctaTexto: 'Quero Recorrer',
    destaque: true,
    badge: 'Mais Solicitado',
  },
  {
    nome: 'Infração Gravíssima',
    preco: 'R$ 120,00',
    descricao:
      'Recurso administrativo para infrações gravíssimas sem efeito suspensivo.',
    ctaTexto: 'Quero Recorrer',
  },
];

const nota =
  'Processos com efeito suspensivo, suspensão (PSDD), cassação (PCDD) e outros casos específicos são orçados individualmente após análise gratuita. Nenhuma surpresa, sempre transparência.';
---

<section
  id="precos"
  class="section-py"
  style="background-color: var(--t-surface-alt);"
>
  <div class="container-wide">
    <!-- Cabeçalho -->
    <div class="text-center mb-4 container-content mx-auto">
      <!-- Badge -->
      <div
        class="inline-flex items-center gap-2 rounded-full px-4 py-1.5 text-sm font-bold mb-6"
        style="background-color: var(--t-secondary); color: var(--t-dark);"
      >
        <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
          <polyline points="20 6 9 17 4 12"/>
        </svg>
        Análise Inicial Gratuita
      </div>

      <h2
        class="font-serif text-display-sm mb-4"
        style="color: var(--t-text-main);"
      >
        Quanto Custa Recorrer da Sua Multa?
      </h2>
      <p class="text-body-lg" style="color: var(--t-text-soft);">
        Valores diretos para os tipos de recurso mais comuns. Para suspensão,
        cassação e outros casos específicos, a análise inicial é gratuita e o
        orçamento é apresentado antes de qualquer compromisso.
      </p>
    </div>

    <!-- Cards de preço -->
    <div class="grid sm:grid-cols-3 gap-6 max-w-3xl mx-auto mb-8">
      {planos.map((p) => (
        <article
          class="rounded-2xl p-7 flex flex-col items-center text-center relative overflow-hidden transition-shadow duration-200 hover:shadow-xl"
          style={`
            background-color: ${p.destaque ? 'var(--t-primary)' : 'var(--t-surface)'};
            border: 2px solid ${p.destaque ? 'var(--t-primary)' : 'var(--t-border)'};
            transform: ${p.destaque ? 'scale(1.04)' : 'scale(1)'};
          `}
        >
          {/* Badge destaque */}
          {p.badge && (
            <span
              class="absolute top-0 left-1/2 -translate-x-1/2 -translate-y-1/2 rounded-full px-4 py-1 text-xs font-black tracking-wide"
              style="background-color: var(--t-secondary); color: var(--t-dark);"
            >
              {p.badge}
            </span>
          )}

          {/* Nome */}
          <h3
            class="font-serif font-bold text-base mb-5 mt-2"
            style={`color: ${p.destaque ? 'rgba(255,255,255,0.75)' : 'var(--t-text-soft)'};`}
          >
            {p.nome}
          </h3>

          {/* Preço */}
          <div
            class="text-4xl font-black mb-1"
            style={`color: ${p.destaque ? 'white' : 'var(--t-primary)'};`}
          >
            {p.preco}
          </div>
          <p
            class="text-xs mb-5"
            style={`color: ${p.destaque ? 'rgba(255,255,255,0.5)' : 'var(--t-text-muted)'};`}
          >
            por recurso
          </p>

          {/* Descrição */}
          <p
            class="text-sm leading-relaxed mb-6 flex-1"
            style={`color: ${p.destaque ? 'rgba(255,255,255,0.75)' : 'var(--t-text-soft)'};`}
          >
            {p.descricao}
          </p>

          {/* CTA */}
          <a
            href={waUrl}
            target="_blank"
            rel="noopener noreferrer"
            class="w-full flex items-center justify-center rounded-xl px-5 py-3.5 text-sm font-bold transition-all duration-200 hover:opacity-90 active:scale-[0.97]"
            style={`
              background-color: ${p.destaque ? 'var(--t-secondary)' : 'var(--t-primary)'};
              color: ${p.destaque ? 'var(--t-dark)' : 'white'};
              min-height: 44px;
            `}
          >
            {p.ctaTexto}
          </a>
        </article>
      ))}
    </div>

    <!-- Nota -->
    <div
      class="max-w-2xl mx-auto rounded-xl p-5 text-center"
      style="background-color: var(--t-surface); border: 1px solid var(--t-border);"
    >
      <p class="text-sm leading-relaxed" style="color: var(--t-text-soft);">
        <strong style="color: var(--t-text-main);">Casos especiais:</strong>{' '}
        {nota}
      </p>
    </div>
  </div>
</section>
```

---

### `src/components/sections/Faq.astro`

```astro
---
const waNumber = import.meta.env.PUBLIC_WA_NUMBER ?? '';
const waMessage = import.meta.env.PUBLIC_WA_MESSAGE ?? '';
const waUrl = `https://wa.me/${waNumber}?text=${encodeURIComponent(waMessage)}`;

const perguntas = [
  {
    q: 'Toda multa pode ser cancelada?',
    a: 'Não. Cada caso é analisado individualmente. Existem multas com chances maiores de sucesso devido a erros técnicos, falhas no auto de infração ou problemas no processo administrativo. Por isso fazemos uma análise técnica antes de qualquer recurso.',
  },
  {
    q: 'Vale a pena recorrer da multa?',
    a: 'Sim, principalmente quando há risco de perda da CNH, pontos acumulados, multa de valor alto ou impacto direto na sua renda. O recurso pode evitar prejuízos financeiros e administrativos significativos.',
  },
  {
    q: 'Vocês garantem vitória no recurso?',
    a: 'Não trabalhamos com promessas irreais. Fazemos uma análise técnica completa e aplicamos a melhor estratégia disponível para aumentar as chances de sucesso. O resultado final depende dos órgãos competentes.',
  },
  {
    q: 'Preciso ir até um escritório?',
    a: 'Não. Todo o atendimento e envio de documentos é feito online pelo WhatsApp ou e-mail. Atendemos motoristas de qualquer estado sem que você precise sair de casa.',
  },
  {
    q: 'Posso continuar dirigindo durante o processo?',
    a: 'Na maioria dos casos, sim. Enquanto houver possibilidade de defesa e o processo estiver em andamento, o motorista normalmente mantém o direito de dirigir. Verificamos isso já na análise inicial.',
  },
  {
    q: 'Quanto tempo demora um recurso?',
    a: 'O prazo varia conforme o órgão responsável e a etapa do processo. Em média, pode levar de algumas semanas a alguns meses. Você é informado sobre o andamento em cada etapa.',
  },
];
---

<section
  id="faq"
  class="section-py"
  style="background-color: var(--t-background);"
>
  <div class="container-wide">
    <div class="container-content mx-auto">
      <!-- Cabeçalho -->
      <div class="text-center mb-10">
        <h2
          class="font-serif text-display-sm mb-4"
          style="color: var(--t-text-main);"
        >
          Perguntas Frequentes
        </h2>
        <p class="text-body-lg" style="color: var(--t-text-soft);">
          Respondemos as dúvidas mais comuns antes que você precise perguntar.
        </p>
      </div>

      <!-- Acordeão -->
      <div class="flex flex-col" role="list">
        {perguntas.map((item, i) => (
          <div
            role="listitem"
            class="faq-item"
            style={`border-bottom: 1px solid var(--t-border); ${i === 0 ? 'border-top: 1px solid var(--t-border);' : ''}`}
          >
            <button
              class="faq-trigger w-full flex items-center justify-between gap-4 py-5 text-left font-semibold text-base cursor-pointer"
              aria-expanded="false"
              style="color: var(--t-text-main); background: none; border: none; padding-inline: 0;"
            >
              <span>{item.q}</span>
              <svg
                class="faq-icon flex-shrink-0 transition-transform duration-300"
                width="20"
                height="20"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2.5"
                stroke-linecap="round"
                stroke-linejoin="round"
                aria-hidden="true"
                style="color: var(--t-primary);"
              >
                <polyline points="6 9 12 15 18 9" />
              </svg>
            </button>

            <div
              class="faq-content overflow-hidden"
              style="max-height: 0; transition: max-height 0.35s ease;"
            >
              <p
                class="pb-5 text-sm leading-relaxed"
                style="color: var(--t-text-soft);"
              >
                {item.a}
              </p>
            </div>
          </div>
        ))}
      </div>

      <!-- CTA pós-FAQ -->
      <div class="text-center mt-10">
        <p class="text-sm mb-4" style="color: var(--t-text-soft);">
          Não encontrou sua dúvida? Fale diretamente com a gente:
        </p>
        <a
          href={waUrl}
          target="_blank"
          rel="noopener noreferrer"
          class="inline-flex items-center gap-2 rounded-xl px-7 py-4 font-bold text-sm text-white transition-all duration-200 hover:opacity-90 active:scale-[0.97]"
          style="background-color: var(--t-primary); min-height: 44px;"
        >
          <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
            <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 0 1-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 0 1-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 0 1 2.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0 0 12.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 0 0 5.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 0 0-3.48-8.413z"/>
          </svg>
          Tirar Minha Dúvida Agora
        </a>
      </div>
    </div>
  </div>
</section>

<script>
  document.querySelectorAll<HTMLButtonElement>('.faq-trigger').forEach((btn) => {
    btn.addEventListener('click', () => {
      const content = btn.nextElementSibling as HTMLElement | null;
      const icon = btn.querySelector<HTMLElement>('.faq-icon');
      const isOpen = btn.getAttribute('aria-expanded') === 'true';

      // Fecha todos os outros
      document.querySelectorAll<HTMLButtonElement>('.faq-trigger').forEach((other) => {
        if (other !== btn && other.getAttribute('aria-expanded') === 'true') {
          other.setAttribute('aria-expanded', 'false');
          const otherContent = other.nextElementSibling as HTMLElement | null;
          const otherIcon = other.querySelector<HTMLElement>('.faq-icon');
          if (otherContent) otherContent.style.maxHeight = '0';
          if (otherIcon) otherIcon.style.transform = 'rotate(0deg)';
        }
      });

      // Toggle atual
      btn.setAttribute('aria-expanded', String(!isOpen));
      if (content) {
        content.style.maxHeight = isOpen ? '0' : content.scrollHeight + 'px';
      }
      if (icon) {
        icon.style.transform = isOpen ? 'rotate(0deg)' : 'rotate(180deg)';
      }
    });
  });
</script>
```

---

### `src/components/sections/CtaFinal.astro`

```astro
---
const waNumber = import.meta.env.PUBLIC_WA_NUMBER ?? '';
const waMessage = import.meta.env.PUBLIC_WA_MESSAGE ?? '';
const waUrl = `https://wa.me/${waNumber}?text=${encodeURIComponent(waMessage)}`;
---

<section
  id="cta-final"
  class="relative overflow-hidden section-py"
  style="background-color: var(--t-primary);"
>
  <!-- Decoração de fundo -->
  <div class="absolute inset-0 pointer-events-none overflow-hidden" aria-hidden="true">
    <div
      class="absolute rounded-full"
      style="width: 400px; height: 400px; top: -100px; left: -100px; background: rgba(255,255,255,0.04);"
    ></div>
    <div
      class="absolute rounded-full"
      style="width: 300px; height: 300px; bottom: -80px; right: -80px; background: rgba(237,189,36,0.1);"
    ></div>
  </div>

  <div class="container-wide relative">
    <div class="container-content mx-auto text-center">
      <!-- Badge -->
      <div
        class="inline-flex items-center gap-2 rounded-full px-4 py-1.5 text-sm font-bold mb-6"
        style="background-color: var(--t-secondary); color: var(--t-dark);"
      >
        <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
          <polyline points="20 6 9 17 4 12"/>
        </svg>
        Análise Gratuita
      </div>

      <!-- Título -->
      <h2
        class="font-serif text-display-sm text-white mb-4"
      >
        Não Deixe sua CNH em Risco. Fale com a Gente Agora.
      </h2>

      <!-- Subtítulo -->
      <p
        class="text-body-lg mb-8"
        style="color: rgba(255,255,255,0.78);"
      >
        Envie sua multa pelo WhatsApp e receba uma análise gratuita com orientação
        sobre as reais chances do seu recurso. Sem compromisso.
      </p>

      <!-- CTA -->
      <a
        href={waUrl}
        target="_blank"
        rel="noopener noreferrer"
        class="inline-flex items-center gap-2 rounded-xl px-8 py-4 font-black text-base transition-all duration-200 hover:opacity-90 active:scale-[0.97] mb-5"
        style="background-color: var(--t-secondary); color: var(--t-dark); min-height: 52px;"
      >
        <svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
          <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 0 1-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 0 1-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 0 1 2.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0 0 12.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 0 0 5.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 0 0-3.48-8.413z"/>
        </svg>
        Analisar Minha Multa Grátis
      </a>

      <!-- Horário -->
      <p class="text-sm" style="color: rgba(255,255,255,0.55);">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true" style="display:inline; vertical-align: middle; margin-right: 4px;">
          <circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/>
        </svg>
        Atendimento de Segunda a Sábado
      </p>
    </div>
  </div>
</section>
```

---

### `src/components/sections/Footer.astro`

```astro
---
import DarkModeToggle from '../ui/DarkModeToggle.astro';

const waNumber = import.meta.env.PUBLIC_WA_NUMBER ?? '';
const waMessage = import.meta.env.PUBLIC_WA_MESSAGE ?? '';
const waUrl = `https://wa.me/${waNumber}?text=${encodeURIComponent(waMessage)}`;

const ano = new Date().getFullYear();
---

<footer
  id="footer"
  style="background-color: #0d1f2e; color: rgba(255,255,255,0.7);"
>
  <!-- Conteúdo principal -->
  <div class="container-wide py-14">
    <div class="grid md:grid-cols-3 gap-10">

      <!-- Coluna 1: Marca + CTA -->
      <div>
        <a href="/" aria-label="Cancela Multas — Início" class="inline-flex items-center gap-1 mb-4">
          <span class="font-serif font-black text-xl" style="color: white;">CANCELA</span>
          <span class="font-serif font-black text-xl" style="color: var(--t-secondary);">MULTAS</span>
        </a>
        <p class="text-sm leading-relaxed mb-6">
          Especialistas em recursos de multas de trânsito e defesa da CNH em todo
          o Brasil. Atendimento 100% online.
        </p>
        <a
          href={waUrl}
          target="_blank"
          rel="noopener noreferrer"
          class="inline-flex items-center gap-2 rounded-xl px-5 py-3 text-sm font-bold text-white transition-all duration-200 hover:opacity-90"
          style="background-color: #25D366; min-height: 44px;"
        >
          <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
            <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 0 1-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 0 1-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 0 1 2.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0 0 12.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 0 0 5.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 0 0-3.48-8.413z"/>
          </svg>
          Falar no WhatsApp
        </a>
      </div>

      <!-- Coluna 2: Contato -->
      <div>
        <h3 class="font-serif font-bold text-base mb-4" style="color: white;">Contato</h3>
        <ul class="flex flex-col gap-3 text-sm list-none p-0 m-0">
          <li class="flex items-center gap-2">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true" style="flex-shrink:0">
              <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07A19.5 19.5 0 0 1 4.69 12a19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 3.77 1.17h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 8.91a16 16 0 0 0 6.29 6.29l.91-.91a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"/>
            </svg>
            <a href="tel:+5548996729999" class="hover:text-white transition-colors" style="color: inherit;">
              +55 48 99672-9999
            </a>
          </li>
          <li class="flex items-center gap-2">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true" style="flex-shrink:0">
              <circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/>
            </svg>
            <span>Segunda a Sábado</span>
          </li>
          <li class="flex items-center gap-2">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true" style="flex-shrink:0">
              <circle cx="12" cy="12" r="10"/>
              <line x1="2" y1="12" x2="22" y2="12"/>
              <path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/>
            </svg>
            <a href="https://cancelamulta.com.br" class="hover:text-white transition-colors" style="color: inherit;">
              cancelamulta.com.br
            </a>
          </li>
        </ul>
      </div>

      <!-- Coluna 3: Avisos legais + Dark mode -->
      <div>
        <div class="flex items-center justify-between mb-4">
          <h3 class="font-serif font-bold text-base" style="color: white;">Transparência</h3>
          <DarkModeToggle />
        </div>
        <div class="flex flex-col gap-3 text-xs leading-relaxed">
          <p>
            Os serviços prestados possuem natureza administrativa e consultiva.
            Cada processo é analisado individualmente, não havendo garantia de
            deferimento ou cancelamento de multas, pois as decisões dependem
            exclusivamente dos órgãos competentes.
          </p>
          <p>
            Trabalhamos com análise técnica, atendimento ético e orientação
            clara sobre as reais possibilidades de cada caso.
          </p>
          <p>
            Todos os dados e documentos enviados pelos clientes são tratados com
            sigilo e segurança, conforme a legislação vigente.
          </p>
        </div>
      </div>
    </div>
  </div>

  <!-- Rodapé inferior -->
  <div
    style="border-top: 1px solid rgba(255,255,255,0.08);"
  >
    <div class="container-wide py-5 flex flex-col sm:flex-row items-center justify-between gap-3 text-xs">
      <p>© {ano} Cancela Multas. Todos os direitos reservados.</p>
      <div class="flex items-center gap-4">
        <a
          href="/politica-de-privacidade"
          class="hover:text-white transition-colors"
          style="color: inherit;"
        >
          Política de Privacidade
        </a>
        <span aria-hidden="true" style="color: rgba(255,255,255,0.2);">|</span>
        <a
          href="/termos-de-uso"
          class="hover:text-white transition-colors"
          style="color: inherit;"
        >
          Termos de Uso
        </a>
      </div>
    </div>
  </div>
</footer>
```

---

## PASSO 8 — PÁGINAS

### `src/pages/index.astro`

```astro
---
import BaseLayout from '../layouts/BaseLayout.astro';
import Header from '../components/sections/Header.astro';
import Hero from '../components/sections/Hero.astro';
import Servicos from '../components/sections/Servicos.astro';
import Diferenciais from '../components/sections/Diferenciais.astro';
import Precos from '../components/sections/Precos.astro';
import Faq from '../components/sections/Faq.astro';
import CtaFinal from '../components/sections/CtaFinal.astro';
import Footer from '../components/sections/Footer.astro';
---

<BaseLayout
  title="Cancela Multas | Recursos de Trânsito e Defesa da CNH Online"
  description="Especialistas em recursos de multas de trânsito e defesa da CNH em todo o Brasil. Proteja sua carteira contra suspensão e cassação com agilidade, transparência e análise técnica detalhada. Análise inicial gratuita!"
>
  <Header />

  <main id="main-content">
    <Hero />
    <Servicos />
    <Diferenciais />
    <Precos />
    <Faq />
    <CtaFinal />
  </main>

  <Footer />
</BaseLayout>
```

---

### `src/pages/politica-de-privacidade.astro`

```astro
---
import BaseLayout from '../layouts/BaseLayout.astro';
import Header from '../components/sections/Header.astro';
import Footer from '../components/sections/Footer.astro';
---

<BaseLayout
  title="Política de Privacidade — Cancela Multas"
  description="Política de Privacidade da Cancela Multas. Saiba como tratamos seus dados pessoais."
>
  <Header />

  <main id="main-content" class="section-py" style="background-color: var(--t-background);">
    <div class="container-content mx-auto">
      <h1
        class="font-serif text-display-sm mb-6"
        style="color: var(--t-text-main);"
      >
        Política de Privacidade
      </h1>

      <p class="text-sm mb-8" style="color: var(--t-text-muted);">
        Última atualização: <!-- TODO: data de vigência, ex: 07 de junho de 2026 -->
      </p>

      <div
        class="prose-custom flex flex-col gap-6 text-sm leading-relaxed"
        style="color: var(--t-text-soft);"
      >
        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            1. Identificação do Responsável
          </h2>
          <p>
            <!-- TODO: Nome completo ou razão social -->
            <strong>Responsável:</strong> Paulo Alexandre Souza Pires<br />
            <!-- TODO: CPF ou CNPJ -->
            <strong>CPF/CNPJ:</strong> [PREENCHER]<br />
            <!-- TODO: Endereço comercial -->
            <strong>Endereço:</strong> [PREENCHER]<br />
            <strong>E-mail de contato:</strong> <!-- TODO: e-mail do responsável -->[PREENCHER]<br />
            <strong>Site:</strong> cancelamulta.com.br
          </p>
        </section>

        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            2. Dados Coletados
          </h2>
          <p>
            Coletamos apenas os dados fornecidos voluntariamente pelo usuário ao
            entrar em contato pelo WhatsApp, formulário ou e-mail, incluindo:
            nome, número de telefone, documentos de trânsito (CNH, auto de
            infração) e informações relacionadas ao caso.
          </p>
        </section>

        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            3. Finalidade do Uso
          </h2>
          <p>
            Os dados são utilizados exclusivamente para prestação do serviço de
            consultoria e recurso administrativo de multas de trânsito, comunicação
            com o cliente e cumprimento de obrigações legais.
          </p>
        </section>

        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            4. Compartilhamento de Dados
          </h2>
          <p>
            Não vendemos, alugamos ou compartilhamos dados pessoais com terceiros,
            exceto quando exigido por lei ou por autoridade competente, ou quando
            estritamente necessário para a prestação do serviço contratado.
          </p>
        </section>

        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            5. Segurança
          </h2>
          <p>
            Adotamos medidas técnicas e organizacionais adequadas para proteger
            os dados pessoais contra acesso não autorizado, perda ou destruição.
          </p>
        </section>

        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            6. Direitos do Titular
          </h2>
          <p>
            Nos termos da Lei Geral de Proteção de Dados (LGPD — Lei 13.709/2018),
            você tem direito a acessar, corrigir, excluir ou portar seus dados.
            Para exercer esses direitos, entre em contato pelo e-mail indicado
            acima.
          </p>
        </section>

        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            7. Cookies
          </h2>
          <p>
            Este site pode utilizar cookies e tecnologias semelhantes para fins
            analíticos (Google Analytics via Google Tag Manager). Você pode
            desativar cookies nas configurações do seu navegador.
          </p>
        </section>

        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            8. Contato
          </h2>
          <p>
            Dúvidas sobre esta política podem ser enviadas para:
            <!-- TODO: e-mail de contato -->
            [PREENCHER E-MAIL]
          </p>
        </section>
      </div>
    </div>
  </main>

  <Footer />
</BaseLayout>
```

---

### `src/pages/termos-de-uso.astro`

```astro
---
import BaseLayout from '../layouts/BaseLayout.astro';
import Header from '../components/sections/Header.astro';
import Footer from '../components/sections/Footer.astro';
---

<BaseLayout
  title="Termos de Uso — Cancela Multas"
  description="Termos de Uso da Cancela Multas. Conheça as condições de uso dos nossos serviços."
>
  <Header />

  <main id="main-content" class="section-py" style="background-color: var(--t-background);">
    <div class="container-content mx-auto">
      <h1
        class="font-serif text-display-sm mb-6"
        style="color: var(--t-text-main);"
      >
        Termos de Uso
      </h1>

      <p class="text-sm mb-8" style="color: var(--t-text-muted);">
        Última atualização: <!-- TODO: data de vigência -->
      </p>

      <div
        class="flex flex-col gap-6 text-sm leading-relaxed"
        style="color: var(--t-text-soft);"
      >
        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            1. Aceitação
          </h2>
          <p>
            Ao utilizar os serviços da Cancela Multas, você concorda com estes
            Termos de Uso. Caso não concorde, não utilize nossos serviços.
          </p>
        </section>

        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            2. Natureza dos Serviços
          </h2>
          <p>
            Os serviços prestados pela Cancela Multas têm natureza
            <strong>administrativa e consultiva</strong>. Não nos responsabilizamos
            pelos resultados das decisões dos órgãos competentes (DETRAN, DENATRAN,
            JARI, CETRAN e afins), que têm autonomia exclusiva para deferir ou
            indeferir recursos.
          </p>
        </section>

        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            3. Ausência de Garantia de Resultado
          </h2>
          <p>
            Não garantimos o cancelamento de multas ou a manutenção da CNH ativa.
            Cada caso é tratado individualmente e o resultado depende de fatores
            externos ao nosso controle. Informamos ao cliente, antes de qualquer
            pagamento, as reais probabilidades do caso.
          </p>
        </section>

        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            4. Responsabilidade do Cliente
          </h2>
          <p>
            O cliente é responsável por fornecer informações verídicas e
            documentos autênticos. A omissão ou falsidade de informações pode
            comprometer o resultado do recurso e exonera a Cancela Multas de
            qualquer responsabilidade.
          </p>
        </section>

        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            5. Pagamento
          </h2>
          <p>
            Os valores são informados antes de qualquer contratação. O pagamento
            é pela prestação do serviço de análise e elaboração do recurso, não
            pelo resultado obtido.
          </p>
        </section>

        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            6. Propriedade Intelectual
          </h2>
          <p>
            Todo o conteúdo deste site — textos, marca, identidade visual — é de
            propriedade exclusiva da Cancela Multas e não pode ser reproduzido
            sem autorização expressa.
          </p>
        </section>

        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            7. Foro
          </h2>
          <p>
            Estes termos são regidos pela legislação brasileira. Eventuais
            litígios serão resolvidos no foro da comarca de
            <!-- TODO: cidade/comarca do responsável --> [PREENCHER CIDADE], SC.
          </p>
        </section>

        <section>
          <h2 class="font-serif font-bold text-lg mb-2" style="color: var(--t-text-main);">
            8. Contato
          </h2>
          <p>
            Dúvidas sobre estes termos:
            <!-- TODO: e-mail de contato --> [PREENCHER E-MAIL]
          </p>
        </section>
      </div>
    </div>
  </main>

  <Footer />
</BaseLayout>
```

---

## PASSO 9 — `public/favicon.svg`

Crie um favicon SVG mínimo com as cores da marca:

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 32 32">
  <rect width="32" height="32" rx="6" fill="#144e74"/>
  <text x="16" y="22" font-family="Arial Black, sans-serif" font-size="16"
        font-weight="900" fill="#edbd24" text-anchor="middle">CM</text>
</svg>
```

---

## PASSO 10 — VERIFICAÇÃO E BUILD

### Checklist pré-build

Execute antes de `npm run build`:

```bash
# 1. Instalar dependências (se ainda não feito)
npm install tailwindcss @tailwindcss/vite @fontsource-variable/inter

# 2. Build de teste
npm run build

# 3. Preview local
npm run preview
```

### Itens a verificar manualmente

| # | Item | Como verificar |
|---|------|----------------|
| 1 | `npm run build` sem erros | Terminal sem erros em vermelho |
| 2 | `tokens.css` com cores reais | Abrir o arquivo e confirmar valores |
| 3 | `.env` preenchido | Checar os 4 campos |
| 4 | `id="hero-section"` no Hero | DevTools → Inspect element |
| 5 | `id="footer"` no Footer | DevTools → Inspect element |
| 6 | `id="main-content"` no main | DevTools → Inspect element |
| 7 | WA flutuante some no Hero | Rolar para o topo e verificar |
| 8 | WA flutuante some no Footer | Rolar até o rodapé e verificar |
| 9 | Header esconde ao rolar ↓ | Rolar rápido para baixo |
| 10 | Dark mode funciona | Clicar no botão lua/sol no footer |
| 11 | Dark mode persiste após reload | Mudar tema, recarregar página |
| 12 | FAQ acordeão abre/fecha | Clicar nas perguntas |
| 13 | Todos os links WA funcionam | Clicar e verificar URL |
| 14 | GTM carregou | DevTools → Network → filtrar "gtm" |
| 15 | Schema.org no `<head>` | DevTools → Elements → procurar `ld+json` |
| 16 | Responsive mobile 375px | DevTools → Device toolbar → 375px |
| 17 | Botões com min-height 44px | DevTools → Computed styles |
| 18 | `politica-de-privacidade` abre | Navegar para `/politica-de-privacidade` |
| 19 | `termos-de-uso` abre | Navegar para `/termos-de-uso` |
| 20 | Sem console errors | DevTools → Console |

---

## PASSO 11 — TODOs DO CLIENTE (preencher antes de publicar)

### Dados obrigatórios nos arquivos legais

Nos arquivos `politica-de-privacidade.astro` e `termos-de-uso.astro`, substituir todos os `[PREENCHER]` com:

| Campo | Dado necessário |
|-------|-----------------|
| CPF ou CNPJ | Documento do responsável legal |
| Endereço | Endereço comercial completo |
| E-mail de contato | E-mail para solicitações de dados |
| Data de vigência | Data de publicação |
| Cidade/comarca | Para cláusula de foro |

### Assets a substituir depois

| Arquivo | Onde usar | Observação |
|---------|-----------|------------|
| `src/assets/hero-photo.webp` | Hero.astro (coluna direita) | Foto profissional do advogado/especialista. Substituir o card de estatísticas pela foto usando `<Image />`. |
| `src/assets/logo.svg` | Header.astro e Footer.astro | Logotipo vetorial. Substituir o texto por `<Image src={import('../assets/logo.svg')} alt="Cancela Multas" width={160} height={40} />` |
| `public/og-image.jpg` | BaseLayout.astro | Imagem 1200×630px para compartilhamento em redes sociais |
| `public/favicon.svg` | Automático via Astro | Já criado no Passo 9; substituir por versão final |

---

## ERROS COMUNS E SOLUÇÕES

### `Cannot find module '@tailwindcss/vite'`
```bash
npm install @tailwindcss/vite
```

### `Cannot find module '@fontsource-variable/inter'`
```bash
npm install @fontsource-variable/inter
```

### Cores não aparecem (página em branco/sem estilo)
Verificar que `global.css` tem `@import "tailwindcss"` como **segunda linha** (após o fontsource).
Verificar que `BaseLayout.astro` importa `'../styles/global.css'` no frontmatter.

### `@utility` não funciona (Tailwind v3 instalado)
```bash
npm install tailwindcss@latest @tailwindcss/vite@latest
```
Confirmar que não existe `tailwind.config.js` na raiz (v4 é CSS-first).

### Dark mode não persiste
Confirmar que o script inline está no `<head>` do `BaseLayout.astro` **antes** de qualquer CSS. O script deve ler `localStorage` e adicionar a classe `.dark` ao `<html>` antes do render.

### WhatsApp flutuante sempre visível / nunca visível
Confirmar os IDs: `id="hero-section"` (seção Hero), `id="footer"` (elemento footer), `id="wa-float"` (botão WA).

### FAQ não abre
Confirmar que o `<script>` do `Faq.astro` está fora do frontmatter (fora dos `---`), no corpo do componente.

---

## RESUMO DE CONTEÚDO (referência rápida)

| Dado | Valor |
|------|-------|
| Marca | CANCELA MULTAS |
| WhatsApp | +55 48 99672-9999 |
| GTM | GTM-M7S2PDFR |
| Domínio | cancelamulta.com.br |
| Atendimento | Segunda a Sábado |
| Primary color | `#144e74` |
| Secondary color | `#edbd24` |
| Frase hero | "Levou Multa ou sua CNH Pode ser Suspensa? A Gente Resolve." |
| Preços | Média R$40 · Grave R$80 · Gravíssima R$120 |
| Serviços | 4 (sem efeito, com efeito, suspensão/cassação, outros) |
| Diferenciais | 6 cards |
| FAQ | 6 perguntas |
| Schema tipo | LocalBusiness |
