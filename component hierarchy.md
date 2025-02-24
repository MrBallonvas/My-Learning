#### [Component hierarchy](https://nextjs.org/docs/app/getting-started/project-structure#component-hierarchy)

The React components defined in special files of a route segment are rendered in a specific hierarchy:
- `layout.js`
- `template.js`
- `error.js` (React error boundary)
- `loading.js` (React suspense boundary)
- `not-found.js` (React error boundary)
- `page.js` or nested `layout.js`