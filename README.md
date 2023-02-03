# streamdeck-intellij

Plugin for using Elgato Stream Deck with IntelliJ IDEA. Based on the
`Stream Deck Plugin Template` by Elgato
([Stream Deck](https://developer.elgato.com/documentation/stream-deck/)).

## Setup for development

### Prerequisites

Make sure the following is set up on your computer:

- Node.js
- Node version manager (nvm)
- Git
- GitHub account with SSH authentication

### Installation

#### Clone the repo

```
git clone git@github.com:pahund/streamdeck-intellij.git
cd streamdeck-intellij
```

#### Setup Node.js

```
nvm use
```

#### Install dependencies

```
yarn
```

#### Install the plugin

Quit the Stream Deck application.

Locate the installed plugin in the Finder/Explorer. You should find a folder
with the extension `.sdPlugin` in the `Plugins` folder.

On macOS, you will find it here:

    /Users/my.user.name/Library/Application Support/com.elgato.StreamDeck/Plugins/

On Windows, you will find it here:

    %appdata%\Elgato\StreamDeck\Plugins\

Set a global variable to the plugin path, e.g.:

    export SD_PLUGINS="/Users/my.user.name/Library/Application Support/com.elgato.StreamDeck/Plugins"

**Note:** Don't use `~` to abbreviate the path to your home directory!

It makes sense to add this to your shell's settings file, e.g. your `*.zshrc`,
so you don't have to set it every time you open a new terminal.

You can now run the `deploy` script:

    yarn deploy

Now start the Stream Deck application again.

## Debugging

You can debug your JavaScript plugin and/or Property Inspector using Google
Chrome's web developer tools. You first need to enable the HTML remote debugger
in Stream Deck.

On Mac:

```
yarn debug-on
```

On Windows, you will need to add a DWORD `html_remote_debugging_enabled` with
value `1` in the registry
`@ HKEY_CURRENT_USER\Software\Elgato Systems GmbH\StreamDeck`.

After you relaunch the Stream Deck app, you can open
[http://localhost:23654](http://localhost:23654/) in Chrome, where you will find
a list of _Inspectable pages_ (plugins). To inspect your plugin, click the
reverse DNS name of your plugin and open Chrome developer tools, where you can
further inspect used components and log messages.

## Original template documentation

### Description

`Stream Deck Plugin Template` is a complete plugin that shows you how to

- load and save settings using Stream Deck's persistent store
- setup and communicate with the Property Inspector
- pass messages directly from Property Inspector to the plugin (and vice versa)
- localize your Property Inspector's UI to another language

### Features

- code written in Javascript
- cross-platform (macOS, Windows)
- localization support
- styled
  [Property Inspector](https://developer.elgato.com/documentation/stream-deck/sdk/property-inspector/)
  included
- Property Inspector contains all required boilerplate code to let you instantly
  work on your plugin's code.

### Quick Start Guide

A short guide to help you get started quickly.

#### Clone the repo

`git clone https://github.com/elgatosf/streamdeck-plugin-template`

#### Replace Name

Rename the folder as well as any references.

`com.elgato.template` with `my.domain.plugin-name`

#### Get the latest library

Be sure `.gitmodules` has been updated to match your new folder name
`my.domain.plugin-name` and then pull the latest libraries.

`git submodule init && git submodule update`

#### Start Coding

You can get started in app.js!

```javascript
const myAction = new Action("com.elgato.template.action");

/**
 * The first event fired when Stream Deck starts
 */
$SD.onConnected(
  ({ actionInfo, appInfo, connection, messageType, port, uuid }) => {
    console.log("Stream Deck connected!");
  }
);

myAction.onKeyUp(({ action, context, device, event, payload }) => {
  console.log("Your key code goes here!");
});

myAction.onDialRotate(({ action, context, device, event, payload }) => {
  console.log("Your dial code goes here!");
});
```
