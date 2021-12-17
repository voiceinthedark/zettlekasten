---
title: publishing-react-app
date: 17/12/17
tags: react reactjs git github gh-pages javascript
---

# **publishing-react-app** 202112170214 
> **d396e4**

In order to publish react apps to github pages, I need to follow the following steps
1. Add gh-pages module as a dependency
   - `npm install gh-pages`
2. set the `homepage` attribute inside `package.json` to equal my github page 
   - `"homepage": "http://voiceinthedark.github.io/repo-name"`
3. set `predeploy` and `deploy` tasks in `package.json`
    ```json
    {
        "predeploy": "npm run build"
        "deploy": "gh-pages -d build"
    }       
    ```
4. Finish the steps by running `npm run deploy`
5. On github pages set the branch of the serving website to be `gh-pages`

### reference
[publishing to github](https://www.freecodecamp.org/news/deploy-a-react-app-to-github-pages/)
