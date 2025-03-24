---
title: "Tailwind CSS Installation Issue"
emoji: "🤔"
type: "tech"
topics: ["Tailwind CSS", "Next.js"]
published: true
date: "2025.03.24"
---

## About

This article describes the issue "Tailwind CSS was not compiled correctly" that I encountered while creating my tech blog site.

## Situation

I created a Next.js app with the following tech stack, consulting with GPT-4:

- TypeScript
- Next.js@15.2.2
- React@19.0.0
- Tailwind CSS@4.0.15

### 1. Install Packages

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

### 2. Create tailwind.config.js

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./src/app/**/*.{js,ts,jsx,tsx}",
    "./src/components/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

### 3. Create global.css

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### 4. Import global.css in app/layout.tsx

```tsx
import "./globals.css";

export const metadata = {
  title: "Your App Title",
  description: "Your App Description",
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

## Issue

When using the Tailwind style "mb-20" in the child page (app/page.tsx), the following statement was not included in the compiled file (.next/static/css/app/page.css):

```css
.mb-20 {
  margin-bottom: calc(var(--spacing) * 20);
}
```

## Solution

The issue was caused by incorrect configuration.
For Tailwind CSS v4.0.0 and above, it should be installed as a plugin using Vite.
I resolved the issue by following the official documentation.
https://tailwindcss.com/docs/installation/using-vite

## Conclusion

- Prioritize official documentation
- Always specify plugin versions when consulting with GPT or other AI assistants

## References

- https://tailwindcss.com/docs/installation/using-vite
- https://blog.ashcolor.jp/blog/programming/tailwind-css-v4-install
