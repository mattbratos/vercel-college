---
title: Chapter 9
order: 9
---

# What are Canonical Tags?


A canonical URL is the URL of the page that search engines think is most representative from a set of duplicate pages on your site.

While you can directly communicate canonical URLs to search engines, they can also decide to group several URLs without you notifying it. This might happen
automatically if Google can find a URL under several different paths.

While Google does a great job at detecting those, their systems work at massive scale and don't cover all edge cases. Canonical tags are an important
aspect to cover for your website to ensure great performance.

If Google finds several URLs that have the same content, it might decide to demote them in search results because they can be considered duplicated.

This also happens across domains, if you run two different websites and post the same content in each one, search engines can decide to pick one of them to
be ranked, or directly demote both.

This is where canonical tags are extremely useful. They let Google know which URLs are the original source of truth and which are duplicated. Lots of
duplicated pages across same or different domains can lead to bad rankings or even penalizations.

Let's imagine that our e-commerce shop allows products to be accessible via example.com/products/phone and example.com/phone.

Both are valid, working URLs, but we use canonical to prevent the detection of duplicate content that we own. If we decided that https://example.com/products/phone should be considered for rankings, we would create a canonical tag:

```html
<link rel="canonical" href="https://example.com/products/phone" />
```

Canonical tags are fundamental in SEO performance, because not only can you create different URLs, but users or marketing tools can also create them.

Imagine that you are running some marketing campaigns on Google, then Google decides to add some UTM parameters. It's possible that this new, unique URL will be indexed by Googlebot so you want to be sure you are still showing your canonical tags to unify duplicate pages.

##### Example

```html
import Head from 'next/head';
 
function IndexPage() {
  return (
    <div>
      <Head>
        <title>Canonical Tag Example</title>
        <link
          rel="canonical"
          href="https://example.com/blog/original-post"
          key="canonical"
        />
      </Head>
      <p>This post exists on two URLs.</p>
    </div>
  );
}
 
export default IndexPage;
```

#### Further Reading

- Google: Consolidate Duplicate URLs
- Next.js: i18n Routing
