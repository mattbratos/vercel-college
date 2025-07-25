---
title: Chapter 26
order: 26
---

# Dynamic Imports for Components


Next, let's turn our attention to a React component that is not needed on the initial page load.

React components can also be imported using dynamic imports, but in this case we use it in conjunction with next/dynamic to make sure it works just like any other React Component.

We will use this method to delay the loading of our modal with the Hello World code sample. By doing this we also remove two further third party libraries from the initial page load.

Open the pages/index.js file and add an import for dynamic from next/dynamic at the beginning of the file:

```
import dynamic from 'next/dynamic';
```

We should also remove this line:

```
import CodeSampleModal from '../components/CodeSampleModal';
```

We can now import it as a dynamic component by adding the following at the beginning of the file:

```javascript
const CodeSampleModal = dynamic(() => import('../components/CodeSampleModal'), {
  ssr: false,
});
```

CodeSampleModal will be the default component returned by ../components/CodeSampleModal. It works like a regular React Component, and you can pass props to it as you normally would.

As we do not need this component on the server, we have used ssr: false to disable it.

Next, we want to defer the loading of this component until it's required by the user. To do this, we can wrap the component in a conditional that checks if the modal should be open, and if so, it will be loaded.

Wrap the CodeSampleModal component like so:

```json
{
  isModalOpen && (
    <CodeSampleModal
      isOpen={isModalOpen}
      closeModal={() => setIsModalOpen(false)}
    />
  );
}
```

Now, when isModalOpen is toggled to true for the first time, the JavaScript required will be requested.

With these optimizations the vitals should now look healthier. Let's run another Lighthouse report in Chrome DevTools to verify.

We are left with this two optimization suggestions:

- Use HTTP2: to solve this problem, we can deploy to somewhere that supports HTTP2 (e.g. Vercel).
- Image elements do no have explicit width and height: This is actually a bug in lighthouse and does not affect site performance.

#### Further Reading

- Next.js: Dynamic Imports Documentation
