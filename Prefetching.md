Prefetching is a way to preload a route in the background before the user visits it.

There are two ways routes are prefetched in Next.js:

- **`<Link>` component**: Routes are automatically prefetched as they become visible in the user's viewport. Prefetching happens when the page first loads or when it comes into view through scrolling.
- **`router.prefetch()`**: The `useRouter` hook can be used to prefetch routes programmatically.

The `<Link>`'s default prefetching behavior (i.e. when the `prefetch` prop is left unspecified or set to `null`) is different depending on your usage of [`loading.js`](https://nextjs.org/docs/app/api-reference/file-conventions/loading). Only the shared layout, down the rendered "tree" of components until the first `loading.js` file, is prefetched and cached for `30s`. This reduces the cost of fetching an entire dynamic route, and it means you can show an [instant loading state](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming#instant-loading-states) for better visual feedback to users.

You can disable prefetching by setting the `prefetch` prop to `false`. Alternatively, you can prefetch the full page data beyond the loading boundaries by setting the `prefetch` prop to `true`.

[[Tools for routing#Link]]
