## Usage

Simply do a `git push`. Hugo static content is generated within the Github runner.

## Installation

*Note:* A detailed tutorial can be found [here](https://blog.x1sec.com/posts/obsidian-to-hugo-github-pages-actions)

1. Place Obsidian vault within a correctly setup [Github pages](https://pages.github.com/) repository. If a [Hugo site](https://gohugo.io/) has not been generated, run `hugo new site`.
2. Create an Github action in the repository, e.g.`.github/workflows/main.yml` with the following contents. Note `vault-path` should be changed to the directory name of the Obsidian vault:

```
name: Deploy from Obsidian notes

on:
  push:
    branches:
      - main

jobs:
  publish_job:
    runs-on: ubuntu-latest
    name: Publish Obsidian notes to Github pages
    steps:
      - uses: x1sec/obsidian-to-hugo-action@main
        with:
          vault-path: myvault
          github-token: ${{ secrets.GITHUB_TOKEN }}
```
3. Ensure the repository workflows permissions for the Github actions on the repository is set to `Read and write`. This can be found in `Settings` under the repository name,  `Actions`, `General`.  [Reference](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository)

## Further details

The conversion from Obsidian Markdown to Hugo is done by running [obsidian-export](https://github.com/zoni/obsidian-export) and adding a modification to the default template layout to fix relative URIs for links and images embedded in the Obsidian notes. Hugo generation uses the workflow [hugo-setup](https://github.com/marketplace/actions/hugo-setup)

Please feel free to reach out to me, `https://twitter.com/haxrob` if you have any issues.
