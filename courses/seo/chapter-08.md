---
title: Chapter 8
order: 8
---

# Special Meta Tags for Search Engines


Meta robot tags are directives that search engines will always respect. Adding these robots tags can make the indexation of your website easier.

There is a difference between directives and suggestions.

Meta robots tags or robots.txt files are directives and will always be obeyed. ** Canonical tags **
are recommendations that Google can decide to obey or not.

There are many options when it comes to page-level meta tags, but the following are examples commonly associated with SEO:

```html
<meta name="robots" content="noindex,nofollow" />
```

The robots tag is probably the most common tag you will see. By default it will have the value index,follow so it does not need to specified, all is also a valid alternative version:

```html
<meta name="robots" content="all" />
```

By setting a robots tag to noindex,nofollow as in the example above, it will indicate to search engines:

- noindex: To not show this page in search results. Omitting noindex will indicate the
page can be indexed and shown in search results. When building a website, you
might not want to index certain pages. Common use cases include settings pages,
internal search pages, policies, and more.
- nofollow: To not follow links on this page. Omitting this will allow robots to crawl and
follow links on this page. Links found on other pages may enable crawling, so
omitting nofollow will allow Google to crawl and follow links on this page. Links found on other pages may enable crawling, so if link A appears in pages X and Y, and X has a nofollow robots tag, but Y doesn't, Google may decide to crawl the link.

Note: You can see a full list of directives in the Google official documentation.

#### Googlebot tag

```html
<meta name="googlebot" content="noindex,nofollow" />
```

You may also see the googlebot tag sometimes. In most
cases the robots is all you will need. The googlebot tag is specific to Google. Use this tag if you
want to have a separate rule for Googlebot, and a general one for the rest of the
search bots.

In the case there is conflicting tags, the more restrictive tag applies.

You may be wondering why we need these tags if you can add URLs to your robots.txt that you do not want crawled. The meta tag gives
you flexibility to mark pages as noindex on demand.

For example, if you apply filters to a products page and you end up with no results, it would be common practice to noindex this page.

URLs that are restricted from bots crawling via robots.txt file will never be crawled by Google, but if the rules are added after pages are already indexed,
pages might remain indexed. The best way to make sure that a page is not indexed is using the noindex tag.

Note: Google can decide to index a page without crawling it. This is extremely rare, but happens when Google wants a page to fulfill a specific search result and has certainty that the page contains what users expect.

#### Google tags

##### nositelinkssearchbox

```html
<meta name="google" content="nositelinkssearchbox" />
```

When users search for your site, Google Search results sometimes display a search box specific to your site, along with other direct links to your site. This tag tells Google not to show the sitelinks search box.

##### notranslate

```html
<meta name="google" content="notranslate" />
```

When Google recognizes that the site contents are not in the language that the user is likely to want to read, Google often provides a link to a translation in the search results.

In general, this gives you the chance to provide your unique and compelling content to a much larger group of users. However, there may be situations where this is not desired. This meta tag tells Google that you don't want them to provide a translation for this page.

#### Example

Now that we have given a run through of some of the common tags you might come across, here is an example of a page putting some of them to use:

```html
import Head from 'next/head';
 
function IndexPage() {
  return (
    <div>
      <Head>
        <title>Meta Tag Example</title>
        <meta name="google" content="nositelinkssearchbox" key="sitelinks" />
        <meta name="google" content="notranslate" key="notranslate" />
      </Head>
      <p>Here we show some meta tags off!</p>
    </div>
  );
}
 
export default IndexPage;
```

As you can see in the example, we are using next/head which is a built-in component for appending elements to the head of a page. To avoid duplicate tags in your head you can use the key property, which will make sure the tag is only rendered once.
