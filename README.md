# Netlify Plugin - Trello Lists

This [plugin](https://www.netlify.com/build/plugins-beta?utm_source=github&utm_medium=plugin-trellolists-pnh&utm_campaign=devex) adds the ability to fetch the JSON data of a public Trello board, and stash the data for each list in a JSON file before your build runs making the data available to your static site generator at build time.

## Overview

This plugin uses anonymous access to the Trello API based on the public URL of the desired board.

You can also configure this plugin to present the gathered data in the appropriate location, so your chosen [static site generator](https://www.netlify.com/blog/2020/04/14/what-is-a-static-site-generator-and-3-ways-to-find-the-best-one/?utm_source=github&utm_medium=plugin-trellolists-pnh&utm_campaign=devex) can leverage it during the build.

## A demo to explore and to clone

- Demo site: https://demo-plugin-trello-lists.netlify.app/
- Demo repo: https://github.com/philhawksworth/demo-netlify-plugin-trello-lists

## Installation

To include this plugin in your site deployment:

### 1. Add the plugin as a dependency

```bash

# Add the plugin as a dependency of your build
npm i --s netlify-plugin-trello-lists

```

### 2. Add the plugin and its options to your netlify.toml

This plugin will fetch Trello data and stash the data prior to the execution of the `build` command you have specified in your Netlify configuration. You can choose which board you want get the data from. Each list will result in an object named in PascalCase corresponding to the list name.


```toml
# Config for the Netlify Build Plugin: netlify-plugin-trello-lists
[[plugins]]
  package = "netlify-plugin-trello-lists"

  [plugins.inputs]

    # The URL of a publicly visible Trello board
    trelloBoardUrl = "https://trello.com/b/twPXW2W1/netlify-plugin-trello-list-info"

    # Location of the JSON data file to be generated
    dataFilePath = "src/_data/trello.json"

    # If the plugin fails, should it do so quietly or cancel the build?
    # "failBuild" | "failPlugin"
    fail = "failBuild"


```

### 3. Configure your Trello board

The Trello board that you choose to use as the source of content must be publicly visible. Future iterations of this plugin _may_ add Trello authentication for private boards.

Each list in the board will yield an object in the JSON file keyed with the name of the list in PascalCase.

Use labels in Trello to identify which cards should be included in the data set you retrieve. Cards labelled `live` will appear in the data set no matter which branch your build ruins in. You can use different labels to allocate cards for inclusion only in builds on corresponding branches. This will allow you to have a notion of "staged" and "live" cards in your content.

For more explanation, see [this article on CSS-Tricks](https://css-tricks.com/using-trello-as-a-super-simple-cms/) which is the inspiration for this plugin.


## Using in local development

To execute this plugin in your local environment and generate a local data set, install the Netlify CLI which will allow you to emulate the Netlify Build process locally (along with some other hand Netlify utilities)

```bash

# install Netlify CLI globally
npm i -g netlify-cli

# create a new Netlify project OR link to an existing one
ntl init
# OR
ntl link

# run the Netlify build in your project repo
ntl build
```
