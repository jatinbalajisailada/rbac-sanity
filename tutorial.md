#  Role-Based Access Control (RBAC)

## Set-Up Sanity Project
First of all install sanity 

`npm create sanity@latest`

## Add an Auth Provider
then NextAuth.js

`npm install next-auth`

then in your project go to src/app > create `.env.local` file where we are gonna keep our environmental variables from auth

in that file terminal run

`npx auth secret`

Now create two variable
1. `AUTH_GITHUB_ID=""`
2. `AUTH_GITHUB_SECRET=""`

we get these 2 from our provider. Go to GitHub developer settings and register a new OAuth app
In HomePage URL paste wesite link `website.com` and in Authorization CallBack URL `website.com/api/auth/callback/github` this is gonna tell how to direct back to our website after authenticating
Now you can see `Client ID` and and create `Client Secret` put these into the above 2 variable in .env.local file

Now we have setuped our environmental variables

Create an `api` folder inside this `src/app` folder [if there isn't one] ; inside `api` folder create `auth` folder [if there isn't one]
create a folder `auth/[...nextauth]` and inside it create a file `route.ts`

In `route.ts` we are gonna put our API Handlers for our authentication which are gonna automatically generated for us.

In `src` create `auth.ts`. This file is very important as all of our next auth configuration is going to exist in this.

We have to install next auth library for this so write the following cmds in `src/auth.ts` :
```
import NextAuth from 'next-auth'
import GitHub from "next-auth/providers/github"

export const {auth, handlers, signIn, signOut} = NextAuth({
  providers = [
    GitHub
  ]
})
```
This will generate all the functions (auth, handlers, signIn, signOut) that we're going to use for authentication in this project.

Go to `app/api/auth/[...nextauth]/route.ts` and copy-paste following:
```
import { handlers } from "@/auth";

export const { GET, POST } = handlers;
```
this means that this route is gonna takecare for our signing in and signing out and callback handling and whatever we setup for our project.
Now go to `page.tsx` and add sign in using GitHub button.
But it gives an error so we will rewrite and organise some code functions in `src/lib/actions/auth.ts` (create file path like this)

`https://github.com/machadop1407/nextjs-15-authentication-next-auth.git` -- reference repo for all this code that need to be written
