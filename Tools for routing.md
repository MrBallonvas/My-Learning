# Link
The following props can be passed to the `<Link>` component:

| Prop                                                                              | Example             | Type             | Required |
| --------------------------------------------------------------------------------- | ------------------- | ---------------- | -------- |
| [`href`](https://nextjs.org/docs/app/api-reference/components/link#href-required) | `href="/dashboard"` | String or Object | Yes      |
| [`replace`](https://nextjs.org/docs/app/api-reference/components/link#replace)    | `replace={false}`   | Boolean          | -        |
| [`scroll`](https://nextjs.org/docs/app/api-reference/components/link#scroll)      | `scroll={false}`    | Boolean          | -        |
| [`prefetch`](https://nextjs.org/docs/app/api-reference/components/link#prefetch)  | `prefetch={false}`  | Boolean or null  | -        |
# useRouter() hook
- `router.push(href: string, { scroll: boolean })`: Perform a client-side navigation to the provided route. Adds a new entry into the [browser’s history](https://developer.mozilla.org/docs/Web/API/History_API) stack.
- `router.replace(href: string, { scroll: boolean })`: Perform a client-side navigation to the provided route without adding a new entry into the [browser’s history stack](https://developer.mozilla.org/docs/Web/API/History_API).
- `router.refresh()`: Refresh the current route. Making a new request to the server, re-fetching data requests, and re-rendering Server Components. The client will merge the updated React Server Component payload without losing unaffected client-side React (e.g. `useState`) or browser state (e.g. scroll position).
- `router.prefetch(href: string)`: [Prefetch](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#2-prefetching) the provided route for faster client-side transitions.
- `router.back()`: Navigate back to the previous route in the browser’s history stack.
- `router.forward()`: Navigate forwards to the next page in the browser’s history stack.
### [Router events](https://nextjs.org/docs/app/api-reference/functions/use-router#router-events)
```TSX
'use client'
 
import { useEffect } from 'react'
import { usePathname, useSearchParams } from 'next/navigation'
 
export function NavigationEvents() {
  const pathname = usePathname()
  const searchParams = useSearchParams()
 
  useEffect(() => {
    const url = `${pathname}?${searchParams}`
    console.log(url)
    // You can now use the current URL
    // ...
  }, [pathname, searchParams])
 
  return '...'
}

import { Suspense } from 'react'
import { NavigationEvents } from './components/navigation-events'
 
export default function Layout({ children }) {
  return (
    <html lang="en">
      <body>
        {children}
 
        <Suspense fallback={null}>
          <NavigationEvents />
        </Suspense>
      </body>
    </html>
  )
}
```
### [Disabling scroll to top](https://nextjs.org/docs/app/api-reference/functions/use-router#disabling-scroll-to-top)
```TSX
'use client'
 
import { useRouter } from 'next/navigation'
 
export default function Page() {
  const router = useRouter()
 
  return (
    <button
      type="button"
      onClick={() => router.push('/dashboard', { scroll: false })}
    >
      Dashboard
    </button>
  )
}
```
# Redirect function
The `redirect` function accepts two arguments:

```
redirect(path, type)
```

|Parameter|Type|Description|
|---|---|---|
|`path`|`string`|The URL to redirect to. Can be a relative or absolute path.|
|`type`|`'replace'` (default) or `'push'` (default in Server Actions)|The type of redirect to perform.|

By default, `redirect` will use `push` (adding a new entry to the browser history stack) in [Server Actions](https://nextjs.org/docs/app/building-your-application/data-fetching/server-actions-and-mutations) and `replace` (replacing the current URL in the browser history stack) everywhere else. You can override this behavior by specifying the `type` parameter.

The `type` parameter has no effect when used in Server Components.
`redirect` does not return a value.
## [Example](https://nextjs.org/docs/app/api-reference/functions/redirect#example)

### [Server Component](https://nextjs.org/docs/app/api-reference/functions/redirect#server-component)

Invoking the `redirect()` function throws a `NEXT_REDIRECT` error and terminates rendering of the route segment in which it was thrown.

```TSX
import { redirect } from 'next/navigation'
 
async function fetchTeam(id: string) {
  const res = await fetch('https://...')
  if (!res.ok) return undefined
  return res.json()
}
 
export default async function Profile({
  params,
}: {
  params: Promise<{ id: string }>
}) {
  const { id } = await params
  const team = await fetchTeam(id)
 
  if (!team) {
    redirect('/login')
  }
 
  // ...
}
```

> **Good to know**: `redirect` does not require you to use `return redirect()` as it uses the TypeScript [`never`](https://www.typescriptlang.org/docs/handbook/2/functions.html#never) type.

### [Client Component](https://nextjs.org/docs/app/api-reference/functions/redirect#client-component)

`redirect` can be used in a Client Component through a Server Action. If you need to use an event handler to redirect the user, you can use the [`useRouter`](https://nextjs.org/docs/app/api-reference/functions/use-router) hook.

```TSX
'use client'
 
import { navigate } from './actions'
 
export function ClientRedirect() {
  return (
    <form action={navigate}>
      <input type="text" name="id" />
      <button>Submit</button>
    </form>
  )
}
```

```TSX
'use server'
 
import { redirect } from 'next/navigation'
 
export async function navigate(data: FormData) {
  redirect(`/posts/${data.get('id')}`)
}
```
