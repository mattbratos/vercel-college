---
title: Chapter 28
order: 28
---

# Optimizing Third-Party Scripts


Many applications rely on third-party JavaScript to include different types of functionality, such as analytics, ads, and customer support widgets. However,
embedding third-party authored code can delay page content from rendering and affect user performance if it is loaded too early.

Next.js provides a built-in Script component that optimizes loading for any third-party script, while giving developers the option to decide when to fetch and execute it.

#### Using the Script Component

Using regular HTML, external scripts would need to be manually appended to next/head:

```html
import Head from 'next/head';
 
function IndexPage() {
  return (
    <div>
      <Head>
        <script src="https://www.googletagmanager.com/gtag/js?id=123" />
      </Head>
    </div>
  );
}
```

With the Next.js Script component, you can add it anywhere in the component without needing to use next/head:

```html
import Script from 'next/script';
 
function IndexPage() {
  return (
    <div>
      <Script
        strategy="afterInteractive"
        src="https://www.googletagmanager.com/gtag/js?id=123"
      />
    </div>
  );
}
```

The Script component introduces a strategy property that allows you to decide when to fetch and execute a script for optimal loading. To not
negatively affect Largest Contentful Paint (LCP), most third-party scripts should be deferred to load after all the contents of a page has finished
loading, either immediately after the page becomes interactive (strategy="afterInteractive") or lazily during browser idle time (strategy="lazyOnload").

#### Further Reading

- Next.js: Script Component
- Next.js: API Reference for next/script
