---
title: Chapter 25
order: 25
---

# Dynamic Imports


In this lesson, we will reduce the amount of JavaScript loaded during initial page load from third-party libraries.

Next.js supports ES2020 dynamic import() for JavaScript. With it, you can import JavaScript modules dynamically and work with them. They also work with server-side rendering (SSR).

Think of dynamic imports as another way to split your code into manageable chunks.

Open the pages/index.js file and remove these two imports at the beginning of the file as we are going to dynamically import them further down the file.

```
import Fuse from 'fuse.js';
import _ from 'lodash';
```

For now we also want to remove:

```javascript
const fuse = new Fuse(countries, {
  keys: ['name'],
  threshold: 0.3,
});
```

Now that we have removed this code, let's set up the search input to use the dynamically imported libraries.

We can replace the input with the following code:

```jsx
<input
  type="text"
  placeholder="Country search..."
  className={styles.input}
  onChange={async (e) => {
    const { value } = e.currentTarget;
    // Dynamically load libraries
    const Fuse = (await import('fuse.js')).default;
    const _ = (await import('lodash')).default;
 
    const fuse = new Fuse(countries, {
      keys: ['name'],
      threshold: 0.3,
    });
 
    const searchResult = fuse.search(value).map((result) => result.item);
 
    const updatedResults = searchResult.length ? searchResult : countries;
    setResults(updatedResults);
 
    // Fake analytics hit
    console.info({
      searchedAt: _.now(),
    });
  }}
/>
```

By using Dynamic Imports, this fixes the "Remove unused JavaScript" issue on page load. This also improves our Time to Interactive (TTI), which helps improve First Input Delay (FID).

Let's run another Lighthouse Report in Chrome DevTools to view our progress.

#### Further Reading

- Next.js: Dynamic Imports Documentation
