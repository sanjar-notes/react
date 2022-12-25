# 347. Deploying Next.js projects
Created Sunday 25 December 2022

There are many options when it comes to deploying a Next.js project.

We'll use [Vercel](https://vercel.com/) -  a hosting provider. It's the same company that created Next.js.

To deploy:
1. Upload the code to GitHub (or any other Git provider)
2. Log in to Vercel, and connect the GitHub repo with Vercel.
3. Enable Network access for all IP addresses - in MongoDB, because Vercel server will now communicate with it, instead of our dev machine.
4. Deploy the project, add environment variables (from `.env` file - as it is absent from the code).

Also - any changes to the `main` branch will trigger a build on Vercel.

There are many more features on Vercel.