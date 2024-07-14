---
title: Github Action
description: Auto-deploy your website using the Static Github action
nextTitle: 'Deploying Your Site'
nextURL: '/docs/guides/deploy'
prevTitle: 'Configurations'
prevURL: '/docs/features/configurations' 
---


<div class="flex items-start px-5 py-5 mb-12 md:mb-5 mt-1 md:translate-y-0 translate-y-5 leading-[18px] bg-neutral-950 border border-yellow-400 rounded-md">
   <img class="hidden w-auto h-12 my-0 mr-5 md:h-20 md:block" src="/assets/images/icons/action.png" />
   <div>
      <h1 class="mb-0 text-base md:text-3xl">Github Action</h1>
      <p class="my-1">Use our github action to deploy your website easily to Github pages. Git push and your changes will automatically be deployed</p>
   </div>
</div>

If you are using one of the templates for your site, you will see a file located at `.github/workflows/static.yml`. This is the Github action you can use to auto-deploy your site. If you are creating a custom template you can copy the <a href="https://github.com/static-templates/starter/blob/main/.github/workflows/static.yml" target="_blank" class="text-yellow-300 underline">Github Action file here</a>.

## Setting up the Github Action to AutoDeploy

After you push your website to a Github repo you will need to navigate to [Settings]->[Pages] and you'll see a dropdown under the **Build and deployment** section.

![Github Pages Dropdown](/assets/images/github-action.png)

You'll want to select Github actions in that dropdown. After you have made those changes your site will be deployed the next time you make a change and push to your `main` branch.

> You may also wish to add a custom domain instead of using a Github subdomain.

## Configuration

If you are not using a custom domain and your website is inside of a subfolder (https://my-org.github.com/my-website/), you will need to make a modification to the **build** step inside of your `static.yml` file.

Locate the section with the following name: `Run the static build step` and you'll see on the next line the run command `run: npx @devdojo/static build`. At the end of this run command you'll need to add the URL of your website, like so:

```
- name: Run the static build step
  run: npx @devdojo/static build https://my-org.github.com/my-website/
```

When your site is built, it will use that URL as an absolute URL for all your assets and images.

## Other ways to host your website

You may want to host your website on another static hosting platform, or on your own server. That's what we'll cover in the next section.