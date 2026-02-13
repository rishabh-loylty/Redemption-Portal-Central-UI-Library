# Redemption Portal Central UI Library

A shared React UI component library for Redemption Portal applications, built with **TypeScript** and **Tailwind CSS**, following **shadcn/ui** patterns (CVA variants, `cn()` utility, design tokens via CSS variables). Optionally integrates cleanly with **HeroUI** in consuming apps.

> Package: `@rishabh-loylty/redemption-portal-ui`

___

## Installation

```bash
npm i @rishabh-loylty/redemption-portal-ui
```

⸻

Setup (Tailwind v4 — Recommended)

Tailwind v4 is “CSS-first”. The key thing you must do is ensure Tailwind scans this package inside node_modules.

1) Ensure your app has Tailwind v4 enabled

If you’re starting fresh:

```
npx create-next-app@latest my-app --ts --eslint --tailwind --app --src-dir
```

2) Ensure shadcn tokens exist in your app (recommended)

This library uses token classes like bg-primary, text-primary-foreground, rounded-md, etc.
The easiest way is to initialize shadcn/ui in the consuming app so the CSS variables are created:

```
npx shadcn@latest init
```

If you already have your own design tokens, you can skip shadcn init — just make sure you define equivalent CSS variables (see Design Tokens below).

3) Add Tailwind v4 @source to your global CSS

Open your app’s global CSS (usually src/app/globals.css) and ensure it contains:

```
@import "tailwindcss";
@source "../node_modules/@rishabh-loylty/redemption-portal-ui";
```

Optional: Setup HeroUI in the consuming app (Tailwind v4)

If your app also uses HeroUI components, you need HeroUI’s Tailwind v4 plugin + provider.

1) Install HeroUI
```
npm i @heroui/react framer-motion
```
2) Create src/hero.ts
```
import { heroui } from "@heroui/react";

export default heroui();
```
3) Wire HeroUI into globals.css

In src/app/globals.css:
```
@import "tailwindcss";

/* Your central UI lib */
@source "../node_modules/@rishabh-loylty/redemption-portal-ui";

/* HeroUI */
@plugin "../hero.ts";
@source "../node_modules/@heroui/theme/dist";
```

4) Add HeroUIProvider (Next.js App Router)

Create src/app/providers.tsx:
```
"use client";

import { HeroUIProvider } from "@heroui/react";

export function Providers({ children }: { children: React.ReactNode }) {
  return <HeroUIProvider>{children}</HeroUIProvider>;
}
```

Wrap your app in src/app/layout.tsx:

```
import "./globals.css";
import { Providers } from "./providers";

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <body>
        <Providers>{children}</Providers>
      </body>
    </html>
  );
}
```

⸻

Usage
```
import { Button } from "@rishabh-loylty/redemption-portal-ui";

export default function Page() {
  return (
    <div style={{ padding: 24 }}>
      <Button>Default</Button>
      <Button variant="outline" style={{ marginLeft: 12 }}>
        Outline
      </Button>
    </div>
  );
}
```

⸻

For Library Maintainers

Publishing
	1.	Bump version:

```
npm version patch
```

	2.	Publish:

```
npm publish --access public
```

Tip: Verify what will be published:
```
npm pack --dry-run
```