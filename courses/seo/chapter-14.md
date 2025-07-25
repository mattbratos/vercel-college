---
title: Chapter 14
order: 14
---

# Metadata


![Example of a SERP snippet with a title and description](./assets/example-of-a-serp-snippet-with-a-title-and-descrip-light.jpg)


Metadata is the abstract of the website's content and is used to attach a title, a description, and an image to the site.

#### Title

The title tag is one of the most important SEO elements for two main reasons:

Firstly, it's what users see when they click to enter your website from search results.

Secondly, it's one of the main elements Google uses to understand what your page is about. Using keywords in the title is recommended because it usually leads to increased improved ranking positions in search engines.

Here's an example:

```html
<title>iPhone 12 XS Max For Sale in Colorado - Big Discounts | Apple</title>
```

This page contains all the main keywords and also makes it attractive for users showing a clear value proposition: Discounts!

#### Description

The description meta tag is another important SEO element, but less so than the title. According to Google, this element is not taken into account for
ranking purposes, but it can affect your click-through-rate on search results.

Use the description meta tag to complement the information in your title. Work in more keywords to the content here if there are some that didn't fit in the
title. These keywords will appear in bold if a user's search contains them.

An example of a description meta tag in HTML:

```html
<meta
  name="description"
  content="Check out iPhone 12 XR Pro and iPhone 12 Pro Max. Visit your local store and for expert advice."
/>
```

This how it looks on the page when it's part of the search engine results page (SERP):

In Next.js, we set the title and description in the Head component. This is how meta title and description tags might look like in Next.js:

```html
import Head from 'next/head';
 
function IndexPage() {
  return (
    <div>
      <Head>
        <title>
          iPhone 12 XS Max For Sale in Colorado - Big Discounts | Apple
        </title>
        <meta
          name="description"
          content="Check out iPhone 12 XR Pro and iPhone 12 Pro Max. Visit your local store and for expert advice."
          key="desc"
        />
      </Head>
      <h1>iPhones for Sale</h1>
      <p>insert a list of iPhones for sale.</p>
    </div>
  );
}
 
export default IndexPage;
```

The Head component can be used on any page in your application to describe or provide information about the page's contents.

#### Open Graph

The Open Graph protocol, originally developed by Facebook, standardizes how metadata is used on any given web
page. You can provide as little or as much information as you would like, but all of the open graph pieces fit together to create a representation of the
site it's attached to.

Other social media companies (like Pinterest, Twitter, LinkedIn, etc), may also use open graph for displaying rich cards when sharing a URL. Twitter also
has tags of its Twitter Cards.

While these Open Graph tags have a lot of similarities with SEO related tags, they do not offer any benefit to search engine rankings, but they are still
recommended to use as people might share your content on social media or private messaging tools such as WhatsApp or Telegram.

You can add Open Graph tags by defining the property attribute in the meta tags inside the Head component. For example:

```html
import Head from 'next/head';
 
function IndexPage() {
  return (
    <div>
      <Head>
        <title>Cool Title</title>
        <meta name="description" content="Checkout our cool page" key="desc" />
        <meta property="og:title" content="Social Title for Cool Page" />
        <meta
          property="og:description"
          content="And a social description for our cool page"
        />
        <meta
          property="og:image"
          content="https://example.com/images/cool-page.jpg"
        />
      </Head>
      <h1>Cool Page</h1>
      <p>This is a cool page. It has lots of cool content!</p>
    </div>
  );
}
 
export default IndexPage;
```

Having a shareable link that offers a description and title, along with a picture that represents the page's content does not have a direct effect on
SEO rankings, but it indirectly increases the clickability of the link, which will ultimately lead to more visitors to your site.

#### Structured Data and JSON-LD

Structured data facilitates the understanding of your pages to search engines. Over the years, there have been several vocabularies in place, but currently the main one is schema.org.

According to the website, schema.org is a "collaborative, community activity with a mission to create, maintain, and promote schemas for structured data on the Internet, on web pages, in email messages, and beyond."

Schema.org's vocabulary can be used with many different encodings, including RDFa, Microdata, and JSON-LD.

Different search engines might adapt different vocabularies within schema.org, and no search engine covers all the use cases described the website's
vocabulary. Be sure to check which vocabularies are accepted in each case.

An example of a what a product page might look like adding the JSON-LD product schema data:

```html
import Head from 'next/head';
 
function ProductPage() {
  function addProductJsonLd() {
    return {
      __html: `{
      "@context": "https://schema.org/",
      "@type": "Product",
      "name": "Executive Anvil",
      "image": [
        "https://example.com/photos/1x1/photo.jpg",
        "https://example.com/photos/4x3/photo.jpg",
        "https://example.com/photos/16x9/photo.jpg"
       ],
      "description": "Sleeker than ACME's Classic Anvil, the Executive Anvil is perfect for the business traveler looking for something to drop from a height.",
      "sku": "0446310786",
      "mpn": "925872",
      "brand": {
        "@type": "Brand",
        "name": "ACME"
      },
      "review": {
        "@type": "Review",
        "reviewRating": {
          "@type": "Rating",
          "ratingValue": "4",
          "bestRating": "5"
        },
        "author": {
          "@type": "Person",
          "name": "Fred Benson"
        }
      },
      "aggregateRating": {
        "@type": "AggregateRating",
        "ratingValue": "4.4",
        "reviewCount": "89"
      },
      "offers": {
        "@type": "Offer",
        "url": "https://example.com/anvil",
        "priceCurrency": "USD",
        "price": "119.99",
        "priceValidUntil": "2020-11-20",
        "itemCondition": "https://schema.org/UsedCondition",
        "availability": "https://schema.org/InStock"
      }
    }
  `,
    };
  }
  return (
    <div>
      <Head>
        <title>My Product</title>
        <meta
          name="description"
          content="Super product with free shipping."
          key="desc"
        />
        <script
          type="application/ld+json"
          dangerouslySetInnerHTML={addProductJsonLd()}
          key="product-jsonld"
        />
      </Head>
      <h1>My Product</h1>
      <p>Super product for sale.</p>
    </div>
  );
}
 
export default ProductPage;
```

In this example, the data is hardcoded as a string, but you can easily pass the data to the addProductJsonLd method to make it fully dynamic.

#### Further Reading

- Open Graph Protocol: Documentation
- Google: Intro to Structured Data
- Google: Product Structured Data
- Google: Rich Results Tester
