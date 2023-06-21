# c272.org

## Overview
Welcome to the repository for my personal website, currently hosted at [c272.org](https://c272.org). This contains all non-theme content (posts, custom layouts, etc.) for this website, as well as workflows for deploying the site to live and staging servers. Everything is built on Hugo, with a custom theme I created for the site, `coffeeline`, which is hosted in a separate repository [here](https://github.com/c272/coffeeline).

## Development
To host a local copy of the site for development, ensure that you have Hugo Extended installed on PATH as `hugo` (you need this for the SASS compilation extensions), and then run the following commands:
```bash
hugo
```

To build the site for deployment to an upstream, you can run the following command:
```bash
hugo publish
```