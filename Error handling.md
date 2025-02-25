Errors can be divided into two categories: **expected errors** and **uncaught exceptions**:
- **Model expected errors as return values**: Avoid using `try`/`catch` for expected errors in Server Actions. Use [`useActionState`](https://react.dev/reference/react/useActionState) to manage these errors and return them to the client.
- **Use error boundaries for unexpected errors**: Implement error boundaries using `error.tsx` and `global-error.tsx` files to handle unexpected errors and provide a fallback UI.

# [Handling Expected Errors](https://nextjs.org/docs/app/building-your-application/routing/error-handling#handling-expected-errors)
### [Handling Expected Errors from Server Actions](https://nextjs.org/docs/app/building-your-application/routing/error-handling#handling-expected-errors-from-server-actions)
Use the `useActionState` hook to manage the state of Server Actions, including handling errors. This approach avoids `try`/`catch` blocks for expected errors, which should be modeled as return values rather than thrown exceptions.
```TSX
'use server'
 
import { redirect } from 'next/navigation'
 
export async function createUser(prevState: any, formData: FormData) {
  const res = await fetch('https://...')
  const json = await res.json()
 
  if (!res.ok) {
    return { message: 'Please enter a valid email' }
  }
 
  redirect('/dashboard')
}
```
Then, you can pass your action to the `useActionState` hook and use the returned `state` to display an error message.
```TSX
'use client'
 
import { useActionState } from 'react'
import { createUser } from '@/app/actions'
 
const initialState = {
  message: '',
}
 
export function Signup() {
  const [state, formAction, pending] = useActionState(createUser, initialState)
  return (
    <form action={formAction}>
      <label htmlFor="email">Email</label>
      <input type="text" id="email" name="email" required />
      {/* ... */}
      <p aria-live="polite">{state?.message}</p>
      <button disabled={pending}>Sign up</button>
    </form>
  )
}
```
### [Handling Expected Errors from Server Components](https://nextjs.org/docs/app/building-your-application/routing/error-handling#handling-expected-errors-from-server-components)

When fetching data inside of a Server Component, you can use the response to conditionally render an error message or [`redirect`](https://nextjs.org/docs/app/building-your-application/routing/redirecting#redirect-function).
```TSX
export default async function Page() {
  const res = await fetch(`https://...`)
  const data = await res.json()
 
  if (!res.ok) {
    return 'There was an error.'
  }
 
  return '...'
}
```

# [Uncaught Exceptions](https://nextjs.org/docs/app/building-your-application/routing/error-handling#uncaught-exceptions)
### [Using Error Boundaries](https://nextjs.org/docs/app/building-your-application/routing/error-handling#using-error-boundaries)
```TSX
'use client' // Error boundaries must be Client Components
 
import { useEffect } from 'react'
 
export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string }
  reset: () => void
}) {
  useEffect(() => {
    // Log the error to an error reporting service
    console.error(error)
  }, [error])
 
  return (
    <div>
      <h2>Something went wrong!</h2>
      <button
        onClick={
          // Attempt to recover by trying to re-render the segment
          () => reset()
        }
      >
        Try again
      </button>
    </div>
  )
}
```
If you want errors to bubble up to the parent error boundary, you can `throw` when rendering the `error` component.
### [Handling Global Errors](https://nextjs.org/docs/app/building-your-application/routing/error-handling#handling-global-errors)
While less common, you can handle errors in the root layout using `app/global-error.js`, located in the root app directory, even when leveraging [internationalization](https://nextjs.org/docs/app/building-your-application/routing/internationalization). Global error UI must define its own `<html>` and `<body>` tags, since it is replacing the root layout or template when active.
```TSX
'use client' // Error boundaries must be Client Components
 
export default function GlobalError({
  error,
  reset,
}: {
  error: Error & { digest?: string }
  reset: () => void
}) {
  return (
    // global-error must include html and body tags
    <html>
      <body>
        <h2>Something went wrong!</h2>
        <button onClick={() => reset()}>Try again</button>
      </body>
    </html>
  )
}
```