---
title: Chapter 7
order: 7
---

# XML Sitemaps


Sitemaps are the easiest way to communicate with Google. They indicate the URLs that belong to your website and when they update so that Google can easily detect new content and crawl your website more efficiently.

Even though XML Sitemaps are the most known and used ones, they can also be created via RSS or Atom, or even via Text files if you prefer maximum simplicity.

A sitemap is a file where you provide information about the pages, videos, and other files on your site, and the relationships between them. Search engines like Google read this file to more intelligently crawl your site.

According to Google:

You might need a sitemap if:

- Your site is really large. As a result, it's more likely Google web crawlers might overlook crawling some of your new or recently updated pages.
- Your site has a large archive of content pages that are isolated or not well linked to each other. If your site pages don't naturally reference each other, you can list them in a sitemap to ensure that Google doesn't overlook some of your pages.
- Your site is new and has few external links to it. Googlebot and other web crawlers navigate the web by following links from one page to another. As a result, Google might not discover your pages if no other sites link to them.
- Your site has a lot of rich media content (video, images) or is shown in Google News. If provided, Google can take additional information from sitemaps into account for search, where appropriate.

While sitemaps are not mandatory for great search engine performance, they can facilitate crawling and indexing to bots and hence your content will be picked up faster and rank accordingly.

It's strongly recommended to use sitemaps and make them dynamic as new content is populated across your website. Static sitemaps are also valid, but they might be less useful to Google as it won't serve for constant discovery purposes.

#### How to Add Sitemaps to a Next.js Project

There are two options:

Manual: If you have a relatively simple and static site, you can manually create a sitemap.xml in the public directory of your project:

```xml
<!-- public/sitemap.xml -->
   <xml version="1.0" encoding="UTF-8">
   <urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
     <url>
       <loc>http://www.example.com/foo</loc>
       <lastmod>2021-06-01</lastmod>
     </url>
   </urlset>
   </xml>
```

Dynamic: If your site is dynamic, you can leverage getServerSideProps to generate an XML sitemap on-demand.

We can create a new page inside the pages directory such as pages/sitemap.xml.js. The goal of this page will be to hit our API to get data that will allow us to know the URLs of our dynamic pages. We will then write an XML file as the response for /sitemap.xml

Here is an example if you could try out for yourself:

```xml
//pages/sitemap.xml.js
const EXTERNAL_DATA_URL = 'https://jsonplaceholder.typicode.com/posts';
 
function generateSiteMap(posts) {
  return `<?xml version="1.0" encoding="UTF-8"?>
   <urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
     <!--We manually set the two URLs we know already-->
     <url>
       <loc>https://jsonplaceholder.typicode.com</loc>
     </url>
     <url>
       <loc>https://jsonplaceholder.typicode.com/guide</loc>
     </url>
     ${posts
       .map(({ id }) => {
         return `
       <url>
           <loc>${`${EXTERNAL_DATA_URL}/${id}`}</loc>
       </url>
     `;
       })
       .join('')}
   </urlset>
 `;
}
 
function SiteMap() {
  // getServerSideProps will do the heavy lifting
}
 
export async function getServerSideProps({ res }) {
  // We make an API call to gather the URLs for our site
  const request = await fetch(EXTERNAL_DATA_URL);
  const posts = await request.json();
 
  // We generate the XML sitemap with the posts data
  const sitemap = generateSiteMap(posts);
 
  res.setHeader('Content-Type', 'text/xml');
  // we send the XML to the browser
  res.write(sitemap);
  res.end();
 
  return {
    props: {},
  };
}
 
export default SiteMap;
```

#### Further Reading

- Google: Learn about Sitemaps
- Google: Overview of crawling and indexing topics
