# 4. Migrating to Vite
Created Sun Sep 24, 2023 at 5:00 PM

github issue: https://github.com/sanjar-notes/react/issues/45
## Situation (ignorable)
You have a React app, created using [create-react-app](https://medium.com/r/?url=https%3A%2F%2Fcreate-react-app.dev%2F) (CRA) project that you wish to migrate to [Vite](https://medium.com/r/?url=https%3A%2F%2Fvitejs.dev%2Fguide%2F).

## Why migrate (ignorable)
CRA is really slow, especially the `npm install` step.

This usually results in failure during free deployments (like [render.com](https://www.render.com)) - due to memory usage and timeouts.

Moving to Vite.js solves this - npm install for projects is very fast, development experience is good and free deployments don't fail.

## Preparation
You have your CRA project. Ok.

We need to add Vite config files to this project. For this, create a new (blank) Vite project -

1. Run `npm create vite` in the terminal.
2. In the prompt - add project name ("hello-world"), select framework as `React` and variant as `JavaScript + SWC`.

## Steps
1. **Rename component** `.js` files to `.jsx`. Util files don't need to be renamed. Just to be clear: a component file means any file having JSX code. [See changes (view GitHub commit diff)](https://medium.com/r/?url=https%3A%2F%2Fgithub.com%2Fexemplar-codes%2Fposts-express-api-app%2Fcommit%2F52a0fe58befad2bda8eacf06383fa6f247fe04ef%3Fdiff%3Dsplit). [Automating the rename (wip)](https://github.com/sanjar-notes/react/issues/46)
2. **Move index.html and change shell files** - move index.html from `public` to `src` and change other "shell" files like App.js, index.js, App.css etc. [See changes](https://medium.com/r/?url=https%3A%2F%2Fgithub.com%2Fexemplar-codes%2Fposts-express-api-app%2Fcommit%2F45274accb63c538bb593354843c5c3c284a6b755%3Fdiff%3Dsplit)
3. **Add vite.config.js, package.json**, package-lock.json - just copy this from the fresh vite project into your CRA project. Replace conflicting files. [See changes](https://medium.com/r/?url=https%3A%2F%2Fgithub.com%2Fexemplar-codes%2Fposts-express-api-app%2Fcommit%2F9134d111c7b5e54ddd2e58c434ec895333df3f82%3Fdiff%3Dsplit)
4. **Handle environment variables (optional** - if your project uses them) - code `process.env.PORT` becomes `import.meta.env.PORT`. Make similar changes at other places. [See changes](https://medium.com/r/?url=https%3A%2F%2Fgithub.com%2Fexemplar-codes%2Fposts-express-api-app%2Fcommit%2Fabd00a755defcc39020494610231ae6d734dfb52)
Handle environment variables (optional - if your project uses them)
5. Run the app - `npm run dev` should work now.
6. Cleanup - delete extra files if any.
7. **Deployment build folder (optional)** - Vite's build folder is named `dist` (as opposed to CRA's `build`). Change  corresponding backend code if needed. [See changes](https://github.com/exemplar-codes/posts-express-api-app/commit/3ea3ae51e9f4e343226f8eec788501533777ba46)

For more info, see the GitHub trail (commits) starting from https://github.com/exemplar-codes/posts-express-api-app/commit/52a0fe58befad2bda8eacf06383fa6f247fe04ef
