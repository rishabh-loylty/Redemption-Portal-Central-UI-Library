# Redemption Portal Central UI Library

This is a central UI library for use across Redemption Portal applications. It is built using React, TypeScript, and Tailwind CSS, following the patterns established by shadcn/ui.

## Installation

Install the package from npm:

```bash
npm i @rishabh-loylty/redemption-portal-ui
```

## Setup

This library requires specific configuration in your consuming application's `tailwind.config.js` to work correctly.

### 1. Configure Tailwind Content Path

Add the path to the library's components in the `content` array of your `tailwind.config.js` file. This ensures Tailwind scans the library's classes and generates the necessary CSS.

```js
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./app/**/*.{js,ts,jsx,tsx}",
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
    // Add the library path
    "./node_modules/@rishabh-loylty/redemption-portal-ui/dist/**/*.js",
  ],
  theme: {
    // ...
  },
  plugins: [],
};
```

### 2. Configure Tailwind Theme

The components in this library use custom theme variables inspired by shadcn/ui (e.g., `bg-primary`, `rounded-lg`). You **must** add these to your own `tailwind.config.js` `theme` object.

Below is the recommended base configuration. You can modify the color values to match your application's design system.

```js
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
module.exports = {
  // ... (content array from above)
  theme: {
    container: {
      center: true,
      padding: "2rem",
      screens: {
        "2xl": "1400px",
      },
    },
    extend: {
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        secondary: {
          DEFAULT: "hsl(var(--secondary))",
          foreground: "hsl(var(--secondary-foreground))",
        },
        destructive: {
          DEFAULT: "hsl(var(--destructive))",
          foreground: "hsl(var(--destructive-foreground))",
        },
        muted: {
          DEFAULT: "hsl(var(--muted))",
          foreground: "hsl(var(--muted-foreground))",
        },
        accent: {
          DEFAULT: "hsl(var(--accent))",
          foreground: "hsl(var(--accent-foreground))",
        },
        popover: {
          DEFAULT: "hsl(var(--popover))",
          foreground: "hsl(var(--popover-foreground))",
        },
        card: {
          DEFAULT: "hsl(var(--card))",
          foreground: "hsl(var(--card-foreground))",
        },
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
      keyframes: {
        "accordion-down": {
          from: { height: "0" },
          to: { height: "var(--radix-accordion-content-height)" },
        },
        "accordion-up": {
          from: { height: "var(--radix-accordion-content-height)" },
          to: { height: "0" },
        },
      },
      animation: {
        "accordion-down": "accordion-down 0.2s ease-out",
        "accordion-up": "accordion-up 0.2s ease-out",
      },
    },
  },
  plugins: [require("tailwindcss-animate")],
};
```

You will also need to define the CSS variables, typically in your global CSS file (e.g., `globals.css`):

```css
/* globals.css */
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;
    --card: 0 0% 100%;
    --card-foreground: 222.2 84% 4.9%;
    --popover: 0 0% 100%;
    --popover-foreground: 222.2 84% 4.9%;
    --primary: 222.2 47.4% 11.2%;
    --primary-foreground: 210 40% 98%;
    --secondary: 210 40% 96.1%;
    --secondary-foreground: 222.2 47.4% 11.2%;
    --muted: 210 40% 96.1%;
    --muted-foreground: 215.4 16.3% 46.9%;
    --accent: 210 40% 96.1%;
    --accent-foreground: 222.2 47.4% 11.2%;
    --destructive: 0 84.2% 60.2%;
    --destructive-foreground: 210 40% 98%;
    --border: 214.3 31.8% 91.4%;
    --input: 214.3 31.8% 91.4%;
    --ring: 222.2 84% 4.9%;
    --radius: 0.5rem;
  }

  .dark {
    /* ... Define dark mode colors here if needed */
  }
}
```

Finally, you will need to install `tailwindcss-animate`:

```bash
npm i tailwindcss-animate
```

## Usage Example

```jsx
import { Button } from "@rishabh-loylty/redemption-portal-ui";

export default function MyPage() {
  return <Button variant="outline">Click Me</Button>;
}
```

---

## For Library Maintainers

### Publishing a New Version

1.  Increment the version number:
    ```bash
    npm version patch # or minor, major
    ```
2.  Publish to npm:
    ```bash
    npm publish --access public
    ```
The `prepublishOnly` script will automatically build the project.