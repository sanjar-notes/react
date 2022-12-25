# 343. More about API routes
Created Sunday 25 December 2022

1. "**JSON serializable" props** - we can only return JSON serializable data as props from `getStaticProps`, `getServerSideProps`.
2. **Fetch API** - `fetch` can be used by server side code too, thanks to Next.js.
3. **Bundle safety** - Code imported in a page file used by server side code (`getStaticProps`, `getServerSideProps` etc) will not be included in the client side bundle. So it's safe to do any computation here.
4. **Endpoint handlers and logic separation** - A good idea is to store the server side code (to get meetups from MongoDB) somewhere outside of `pages`, and use that function inside `pages/index.js`. This is similar to storing shared components outside of `pages`. One can also simply write the server side code (to get meetups) directly inside `getStaticProps`, but that's against DRY, assuming we need to fetch all meetups at multiple places in our server side code.