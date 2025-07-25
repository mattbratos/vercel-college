---
title: Chapter 11
order: 11
---

# Rendering Strategies


#### Static Site Generation (SSG)

Static site generation is where your HTML is generated at build time. This HTML is then used for each request. Static site generation is probably the best type of rendering strategy for SEO as not only do you have all the HTML on page load because it's pre-rendered, but it also helps with page performance – now another ranking factor when it comes to SEO.

#### Server-Side Rendering (SSR)

Like SSG, Server-Side Rendering (SSR) is pre-rendered, which also makes it great for SEO. Instead of being generated at build time, as in SSG, SSR's HTML is generated at request time. This is great for when you have pages that are very dynamic.

#### Incremental Static Regeneration (ISR)

If you have a very large amount of pages, generating them all at build time may not be feasible. Next.js allows you to create or update static pages after you have built your site.

Incremental Static Regeneration enables developers and content editors to use static generation on a per-page basis, without needing to rebuild the entire site. With ISR, you can retain the benefits of static while scaling to millions of pages.

#### Client Side Rendering (CSR)

Client-Side Rendering allows developers to make their websites entirely rendered in the browser with JavaScript. On initial page load a single HTML file is generally served with little to no content until you fetch the JavaScript and the browser compiles everything.

As we commented above, in general Client-Side Rendering is not recommended for optimal SEO.

CSR is perfect for data heavy dashboards, account pages or any page that you do not require to be in any search engine index.

#### Summary

The most important thing for SEO is that page data and metadata is available on page load without JavaScript. In this case SSG or SSR are going to be your
best options.

One of the major strengths of Next.js is that each one of the above rendering methods can be done on a per-page basis. You might want your blog posts
statically generated, your customers account dashboard client side rendered and then perhaps you have a news feed you want to server-side render.

#### Further Reading

- Next.js: Data Fetching
- Smashing Magazine: A Complete Guide to Incremental Static Regeneration with Next.js
- Vercel: Next.js: Server-side Rendering vs. Static Generation
