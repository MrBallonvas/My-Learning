### [Nested routes](https://nextjs.org/docs/app/getting-started/project-structure#nested-routes)

| example         | description          |
| --------------- | -------------------- |
| `folder`        | Route segment        |
| `folder/folder` | Nested route segment |
### [Dynamic routes](https://nextjs.org/docs/app/getting-started/project-structure#dynamic-routes)

| example                                                                                                                     | description                      |
| --------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
| [`[folder]`](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes#convention)                       | Dynamic route segment            |
| [`[...folder]`](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes#catch-all-segments)            | Catch-all route segment          |
| [`[[...folder]]`](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes#optional-catch-all-segments) | Optional catch-all route segment |
### [Route Groups and private folders](https://nextjs.org/docs/app/getting-started/project-structure#route-groups-and-private-folders)

| example                                                                                             | description                                      |
| --------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| [`(folder)`](https://nextjs.org/docs/app/building-your-application/routing/route-groups#convention) | Group routes without affecting routing           |
| [`_folder`](https://nextjs.org/docs/app/getting-started/project-structure#private-folders)          | Opt folder and all child segments out of routing |
