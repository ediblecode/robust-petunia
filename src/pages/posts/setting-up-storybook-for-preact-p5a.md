---
title: Setting up Storybook for Preact
date: '2018-09-02T00:00:00.000Z'
excerpt: >-
  Update 2019/06/30: Storybook now has an option via the CLI to install for
  Preact. For more info see P...
thumb_img_path: >-
  https://res.cloudinary.com/practicaldev/image/fetch/s--AMjsJsC0--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://thepracticaldev.s3.amazonaws.com/i/9zm6yatidby4ls11xzeg.png
comments_count: 5
positive_reactions_count: 22
tags:
  - preact
  - storybook
  - javascript
  - ui
canonical_url: 'https://www.iamdeveloper.com/posts/setting-up-storybook-for-preact-p5a/'
template: post
---


Update 2019/06/30: Storybook now has an option via the CLI to install for Preact. For more info see [Preact for Storybook](https://storybook.js.org/docs/guides/guide-preact).TLDR 
`npx -p @storybook/cli sb init --type preact`
.

In my last Storybook post, [Getting Started with Storybook for React](https://dev.to/nickytonline/getting-started-with-react-storybook-9jh), I showed you how to install Storybook for React and gave a quick breakdown of what all the pieces were. I suggest giving that a quick read before continuing here.

In this post, I’ll show you how to get React Storybook up and running with Preact. The assumption is that the project you want to add [Storybook](https://storybook.js.org) to already has [Preact](https://github.com/developit/preact) installed as a dependency.

1. A temporary step is to first install React, so run 
`npm install react`

2. If you have npx installed, run 
`npx @storybook/cli`
 (most people should have this if you’re on a newer version of node). If not run 
`npm install @storybook/cli -g`
.
3. Next from the command line, run 
`getstorybook`

4. This will install all the dependencies you need to run Storybook.
5. Now let’s uninstall 
`react`
 from our dependencies as we want to use preact!
6. Next we need to install [preact-compat](https://github.com/developit/preact-compat) so that Preact will play nicely with Storybook. If you need preact-compat as a dependency for other react libraries, install it to dependencies, 
`npm install preact-compat`
. Otherwise install it as a dev depency, i.e. 
`npm install preact-compat -D`

7. Almost there!
8. The last thing we need to do is tell [webpack](https://webpack.js.org) (what Storybook uses under the hood), to use preact-compat. To do this, we need to create a custom webpack configuration file for Storybook. Lucky for us, Storybook supports this out of the box. In the root folder where your package.json file is, there will be a new folder called 
`.storybook`
. In there it contains files related to Storybook configuration. Create a new file in there called 
`webpack.config.js`
 and paste the following contents and save the file.


```javascript
module.exports = {
  resolve: {
    extensions: [".js", "jsx"],
    alias: {
      react: "preact-compat",
      "react-dom": "preact-compat"
    }
  }
};
```


Note that this is a super bare bones webpack configuration. You can add anything else here you may need just like a regular webpack configuration file.

1. Storybook will create some demo stories for you found in the root folder of your app at 
`./stories/index.stories.js`

2. Open this file and remove the React reference and replace it with 
`import { h } from "preact";`

3. All that’s left to do is run 
`npm run storybook`
 and navigate to Storybook in a browser.

![Screenshot of Storybook in action](https://www.iamdeveloper.com/storybook-cc90189bb245b5d5bdea02cbff77fd3c.gif)

## Extras

- If you want to see an example of the final result, have a look at [my first commit to the dev.to repo](https://github.com/thepracticaldev/dev.to/commit/6a8df8c8ddec739280325c0000d6d32593f70ed0) I made in March of this year.

- I haven’t had time yet, but I was discussing with the Storybook maintainers about potentially having a config for Preact out of the box.


<iframe class="liquidTag" src="https://dev.to/embed/devcomment?args=4ccd" style="border: 0; width: 100%;"></iframe>


Maybe I’ll get to it at some point, but if you’re interested, by all means go for it. 🙃

*[This post is also available on DEV.](https://dev.to/nickytonline/setting-up-storybook-for-preact-p5a)*


<script>
const parent = document.getElementsByTagName('head')[0];
const script = document.createElement('script');
script.type = 'text/javascript';
script.src = 'https://cdnjs.cloudflare.com/ajax/libs/iframe-resizer/4.1.1/iframeResizer.min.js';
script.charset = 'utf-8';
script.onload = function() {
    window.iFrameResize({}, '.liquidTag');
};
parent.appendChild(script);
</script>    
