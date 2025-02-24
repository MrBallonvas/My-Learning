## Server components
### fetch
 To fetch data with the `fetch` API, turn your component into an asynchronous function, and await the `fetch` call. For example:
```TSX
export default async function Page() {  
	const data = await fetch('https://api.vercel.app/blog')  
	const posts = await data.json()
	return (
		<ul>
			{posts.map((post) => (
				<li key={post.id}>
					{post.title}
					</li>
		    ))}
		</ul>
	)
}
```
### ORM
 You can fetch data with an ORM or database by turning your component into an asynchronous function, and awaiting the call:
```TSX
import { db, posts } from '@/lib/db'
 
export default async function Page() {
	const allPosts = await db.select().from(posts)
	return (
	<ul>
	{allPosts.map((post) => (
		<li key={post.id}>
			 {post.title}
		</li>
	))}
	</ul>
)}
```
## Client components
### hook `use`
You can use React's [`use` hook](https://react.dev/reference/react/use) to [stream](https://nextjs.org/docs/app/getting-started/fetching-data#streaming) data from the server to client. Start by fetching data in your Server component, and pass the promise to your Client Component as prop:
```TSX
import Posts from '@/app/ui/posts'
import { Suspense } from 'react'

export default function Page() {
	// Don't await the data fetching function
	const posts = getPosts()
	return (
		<Suspense
			fallback={
				<div>Loading...</div>
			}
		>
			<Posts posts={posts} />
		</Suspense>
	)
}
```

Then, in your Client Component, use the `use` hook read the promise:

```TSX
'use client'
import { use } from 'react'
export default function Posts(
	{posts}: {
		posts: Promise<{
			id: string;
			title: string
		} []>}
	) {
	const allPosts = use(posts)
	return (
		<ul>
			{
				allPosts.map((post) => (
					<li key={post.id}>
						{post.title}
					</li>
				))
			}
		</ul>
	)
}
```

In the example above, you need to wrap the `<Posts />` component in a [`<Suspense>` boundary](https://react.dev/reference/react/Suspense). This means the fallback will be shown while the promise is being resolved. Learn more about [streaming](https://nextjs.org/docs/app/getting-started/fetching-data#streaming).
### custom hook `useSWR`
You can use a community library like [SWR](https://swr.vercel.app/) or [React Query](https://tanstack.com/query/latest) to fetch data in Client Components. These libraries have their own semantics for caching, streaming, and other features. For example, with SWR:
```TSX
'use client'
import useSWR from 'swr'
 
const fetcher = (url) => fetch(url).then((r) => r.json())
 
export default function BlogPage() {
  const { data, error, isLoading } = useSWR(
    'https://api.vercel.app/blog',
    fetcher
  )
 
  if (isLoading) return <div>Loading...</div>
  if (error) return <div>Error: {error.message}</div>
 
  return (
    <ul>
      {data.map((post: { id: string; title: string }) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  )
}
```
