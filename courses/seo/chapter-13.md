---
title: Chapter 13
order: 13
---

# URL Structure


URL Structure is an important part of an SEO strategy. While Google doesn't disclose which weight each part of SEO has, great URLs are considered a best practice no matter if they are a big or small ranking factor in the end.

You might want to follow some principles:

- Semantic: It's best to use URLs that are semantic, meaning that they use words instead of IDs or random numbers. Example: /learn/basics/create-nextjs-appis better than /learn/course-1/lesson-1
- Patterns that are logical and consistent: URLs should follow some sort of pattern that is consistent among pages. For example, you want to have a folder that groups all product pages, instead of having different paths for each product that you have.
- Keyword focused: Google still bases a considerable part of their systems on the keywords a website contains. You might want to use keywords in your URLs to facilitate understanding the purpose of the pages.
- Not parameter-based: Using parameters to build your URLs is generally not a good idea. They are not semantic in most cases, and search engines might confuse them and demote their rankings in results.

#### How are Routes Defined in Next.js?

Next.js uses file-system routing built on the file-system routing built on the concept of pages. When a file is added to
the pages directory, it is automatically available as a route. The files and folders inside the pages directory can be used to define most common patterns.

Let's take a look at a couple of simple URLs and how you would add them to
your Next.js router:

- Homepage: https://www.example.com → pages/index.js
- Listings: https://www.example.com/products → pages/products.js or pages/products/index.js
- Detail: https://www.example.com/products/product → pages/products/product.js

For a blog or e-commerce site you will likely want to use the product ID or
blog name as the slug for the URL. This is called dynamic routing:

- Product: https://www.example.com/products/nextjs-shirt → pages/products/[product].js
- Blog: https://www.example.com/blog/seo-in-nextjs → pages/blog/[blog-name].js

To use dynamic routing, you can add brackets to a page name inside your products or blogs subfolder.

Here's an example of a page optimized for this using SSG:

```html
// pages/blog/[slug].js
 
import Head from 'next/head';
 
export async function getStaticPaths() {
  // Call an external API endpoint to get posts
  const res = await fetch('https://www.example.com/api/posts');
  const posts = await res.json();
 
  // Get the paths we want to pre-render based on posts
  const paths = posts.map((post) => ({
    params: { slug: post.slug },
  }));
  // Set fallback to blocking. Now any new post added post build will SSR
  // to ensure SEO. It will then be static for all subsequent requests
  return { paths, fallback: 'blocking' };
}
 
export async function getStaticProps({ params }) {
  const res = await fetch(`https://www.example.com/api/blog/${params.slug}`);
  const data = await res.json();
 
  return {
    props: {
      blog: data,
    },
  };
}
 
function BlogPost({ blog }) {
  return (
    <>
      <Head>
        <title>{blog.title} | My Site</title>
      </Head>
      <div>
        <h1>{blog.title}</h1>
        <p>{blog.text}</p>
      </div>
    </>
  );
}
 
export default BlogPost;
```

Here's another example using SSR:

```html
// pages/blog/[slug].js
 
import Head from 'next/head';
function BlogPost({ blog }) {
  return (
    <div>
      <Head>
        <title>{blog.title} | My Site</title>
      </Head>
      <div>
        <h1>{blog.title}</h1>
        <p>{blog.text}</p>
      </div>
    </div>
  );
}
 
export async function getServerSideProps({ query }) {
  const res = await fetch(`https://www.example.com/api/blog/${query.slug}`);
  const data = await res.json();
 
  return {
    props: {
      blog: data,
    },
  };
}
 
export default BlogPost;
```

#### Further Reading

- Next.js: Introduction to Routing
- Next.js: Pages
- Next.js: Dynamic Routing
