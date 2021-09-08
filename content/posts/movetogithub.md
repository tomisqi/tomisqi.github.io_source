+++
title = "Move to GitHub pages"
description = ""
tags = [
    "web", "github"
]
date = "2021-09-01"
+++

### Now on GitHub pages!
It took some work, but I now moved this site to GitHub pages. I am using an automated github action that builds and deploys the site.

### Two repositories
I am using a [source](https://github.com/tomisqi/tomisqi.github.io_source) repository to store the "source" of the website and a [built site](https://github.com/tomisqi/tomisqi.github.io) repository to store the built site. When I do changes, I only push to the "source" repository and a github action takes care of building the site using [Hugo](https://gohugo.io/) and pushing the built content into the "built site" repository. 

### Problems
- **Problem** I initially used a single repository, but Hugo places the built site in public/ which means that one had to go to site.github.io/public to access the front page. Also links in the site were broken.<br>
  **Solution**  As exaplained above, create two repositories: one in which the "source" is stored, and another one where the "built site" is stored.

- **Problem** I had trouble making the github action run the deploy job based on the recommendation in [here](https://gohugo.io/hosting-and-deployment/hosting-on-github/).<br>
  **Solution** I had to remove "if: github.ref == 'refs/heads/main'" from the action. I also had to indicate that it should deploy to an external repository. See final [GitHub action](https://github.com/tomisqi/tomisqi.github.io_source/blob/master/.github/workflows/gh-pages.yml).

- **Problem** I was getting an error in the GitHub action which said that it was not allowed to push to an external repository.<br>
  **Solution** As explained [here](https://github.com/marketplace/actions/github-pages-action#%EF%B8%8F-deploy-to-external-repository-external_repository), you need to use a personal token. But this was not straightfoward. I had to go to settings in the "source" repository and create a new secret called "PERSONAL_TOKEN" and paste the contents of the personal token in my GitHub Settings.

- **Problem** Images in raw html where broken. Example `<"img src="images/image.png"/>` did not work any longer.<br>
  **Solution** This was not actually due to GitHub, but instead due to a new version of Hugo. I had to add the following to config.toml: `[markup.goldmark.renderer]unsafe= true`

### Moving Forward
I plan to replace the current theme of this site with something new.