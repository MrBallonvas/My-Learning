Next.js has an **in-memory client-side cache** called the [Router Cache](https://nextjs.org/docs/app/building-your-application/caching#client-side-router-cache). As users navigate around the app, the React Server Component Payload of [prefetched](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#2-prefetching) route segments and visited routes are stored in the cache.

This means on navigation, the cache is reused as much as possible, instead of making a new request to the server - improving performance by reducing the number of requests and data transferred.

Learn more about how the [Router Cache](https://nextjs.org/docs/app/building-your-application/caching#client-side-router-cache) works and how to configure it.