# 347. Deploying Next.js projects
Created Sunday 25 December 2022

## Building - manual
1. Copy the project code to a server.
2. Run `npm run build`.
3. To start Next.js server `npm start`

That's it.

Mentioning this in case I want to deploy manually, using Amazon EC2 (or something similar).

Of course, Next.js is a fullstack framework, so we need a dynamic server. But, if all we want is SSG - no unseen dynamic route SSG, ISR, SSR or API routes, a static server will suffice. In this case all we need is `.next` folder generated after the build. 

FIXME - how to up a static server for a Next project? Do it later.


## Build, deploy and basic CI/CD - Vercel
There are many options when it comes to deploying a Next.js project.

We'll use [Vercel](https://vercel.com/) -  a hosting provider. It's the same company that created Next.js.

To deploy:
1. Upload the code to GitHub (or any other Git provider)
2. Log in to Vercel, and connect the GitHub repo with Vercel.
3. Enable Network access for all IP addresses - in MongoDB, because Vercel server will now communicate with it, instead of our dev machine.
4. Deploy the project, add environment variables (from `.env` file - as it is absent from the code).

Also - any changes to the `main` branch will trigger a build on Vercel.

There are many more features on Vercel.