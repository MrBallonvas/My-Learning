The special file `loading.js` helps you create meaningful Loading UI with [React Suspense](https://react.dev/reference/react/Suspense). With this convention, you can show an [instant loading state](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming#instant-loading-states) from the server while the content of a route segment loads. The new content is automatically swapped in once rendering is complete.
Create a loading state by adding a `loading.js` file inside a folder.

![loading.js special file](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Floading-special-file.png&w=3840&q=75)

```TSX
export default function Loading() {
  // You can add any UI inside Loading, including a Skeleton.
  return <LoadingSkeleton />
}
```

In the same folder, `loading.js` will be nested inside `layout.js`. It will automatically wrap the `page.js` file and any children below in a `<Suspense>` boundary.

![loading.js overview](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Floading-overview.png&w=3840&q=75)
