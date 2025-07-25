---
title: Chapter 24
order: 24
---

# Automatic Image Optimization


#### Unoptimized Images

Using regular HTML, we have added our Hero image like so:

```
<img src="large-image.jpg" alt="Large Image" />
```

However, this means we have to manually optimize a few things like:

- Ensuring our image is responsive on different screen sizes.
- Optimizing our images with a third-party tool or library.
- Lazy-loading images as they enter the viewport

#### The Image Component

Next provides a Image component that can handle these optimizations out-of-the-box for us.

next/image is an extension of the HTML img element, evolved for the modern web.

This means that resizing, optimizing, and serving images in modern formats like WebP (when the browser supports it) can be done automatically using next/image.

The component avoids shipping large images to devices with a smaller viewport and allows Next.js to adopt future image formats and serve those images to
browsers that support them.

Automatic Image Optimization works with any image source. Even if the image is hosted by an external data source, like a CMS, it can still be optimized.

#### How does Automatic Image Optimization Work?

##### On-demand Optimization

Instead of optimizing images at build time, Next.js optimizes images on-demand as users request them. Unlike static site generators and static-only solutions, build times don't increase, whether shipping ten images or ten million images.

##### Lazy Loaded Images

Images are lazy loaded by default. Page speed won't be penalized for images
housed outside of the viewport. Images only load when they come into view.

##### Avoids CLS

Images are always rendered to avoid Cumulative Layout Shift (CLS).

#### Using the Image Component

Let's update the app using next/image to display our hero image. The height and width props should be the desired rendering size, with an aspect ratio identical to the source image.

Open the pages/index.js file and add an import for

Image from next/image at the beginning of the file:

```
import Image from 'next/image';
```

Then, replace the hero img with the Image component:

```jsx
// Before
<img src="large-image.jpg" alt="Large Image" />
 
// After
<Image src="/large-image.jpg" alt="Large Image" width={3048} height={2024} />
```

There's also an image in the footer. Let's replace this as well:

```jsx
// Before
<img src="/vercel.svg" alt="Vercel Logo" />
 
// After
<Image src="/vercel.svg" alt="Vercel Logo" width={72} height={16} />
```

Finally, run another Lighthouse report in Chrome DevTools and compare your results.

#### Further Reading

- Next.js: Automatic Image Optimization Documentation
- Next.js: API Reference for next/image
