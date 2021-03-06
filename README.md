# What is this?
Scram.js offers a simple way to use web components to write server-side code. If you have not heard of web components, then please [start learning today](http://webcomponents.org/). Web components offer a way to modularize and package functionality into reusable components that can be easily shared and composed to create entire applications. Currently they have been used mostly for front-end web development. Well, what about the back-end? Web components are not only useful for visual components, as the [Google Polymer project](https://www.polymer-project.org/1.0/) has shown us. Now you can build APIs and other server-side applications, leveraging the same declarativeness of the front-end world. 

## Server-side Web Components
This repo only offers access to the runtime necessary to use server-side web components. To actually begin building applications, you'll need components to work with:

* Express Web Components: https://github.com/scramjs/express-web-components

## Examples
Here are some example Express.js apps that have been rewritten with web components:
* https://github.com/scramjs/rest-api-express
* https://github.com/scramjs/node-api

## Development Installation
Scram.js leverages Electron to provide a runtime for server-side web components. The only dependency is Electron and Node.js, and you are free to install any compatible version: 

```
npm install --save electron-prebuilt
npm install --save scram-engine
```

## Production Installation
There are a few more considerations in a production environment. Since Electron needs a graphical environment for rendering on headless Linux® machines, you may need to install Xvfb to provide a display server.

On Ubuntu: `sudo apt-get install xvfb`

Electron might require one or more of the following libraries to be installed on certain Ubuntu systems: 

```
libgtk2.0-0
libnotify-bin
Libgconf-2-4
```

### Dokku
Scram.js works well with [Dokku](http://dokku.viewdocs.io/dokku/). Dokku provides a personal PaaS, making it easy to deploy to a production environment.
* Follow the [official documentation](http://dokku.viewdocs.io/dokku/installation/) to install Dokku
* Install this [Dokku plugin](https://github.com/F4-Group/dokku-apt) to allow Dokku to automatically install Xvfb and other packages your application might need
* Add a file to the root directory of your app called `apt-packages`
* List the packages you would like Dokku to install: e.g. xvfb libgtk2.0-0 libnotify-bin Libgconf-2-4
* Ensure that the dependencies are listed correctly in your app's package.json
* Add a `start` script in your app's package.json for Dokku to use to start your application
* Add an `engines` property to your app's package.json to specify the version of node Dokku will use to run your app
* For a full working example of an application deployed with Dokku, see the [Dokku Example](https://github.com/scramjs/dokku-example)

## Usage
### Development
Provide Electron with the main.js script from this repo and then the path to your starting html file from the root directory of your app:

`node_modules/.bin/electron node_modules/scram-engine/main.js index.html`

It might be convenient to create a script in your package.json:

```
{
  "name": "awesome-repo",
  "version": "2.4.2",
  "scripts": {
    "start": "electron node_modules/scram-engine/main.js index.html"
  }
}
```

To open up an Electron window for access to the dev tools, add the `-d` option:

`node_modules/.bin/electron node_modules/scram-engine/main.js index.html -d`

or

```
{
  "name": "awesome-repo",
  "version": "2.4.2",
  "scripts": {
    "start": "electron node_modules/scram-engine/main.js index.html -d"
  }
}
```

### Production
You need to add the xvfb-run command in front of all other commands on headless Linux machines:

`xvfb-run node_modules/.bin/electron node_modules/scram-engine/main.js index.html`

It might be convenient to create a script in your package.json:

```
{
  "name": "awesome-repo",
  "version": "2.4.2",
  "scripts": {
    "start": "xvfb-run electron node_modules/scram-engine/main.js index.html",
    "dev": "electron node_modules/scram-engine/main.js index.html",
    "dev-window": "electron node_modules/scram-engine/main.js index.html -d"
  },
  "engines": {
    "node": "6.0.0"
  }
}
````

## Compatibility and Testing
Only manually tested at the moment. PR with tests if you'd like :)

Node.js is a trademark of Joyent, Inc. and is used with its permission. We are not endorsed by or
affiliated with Joyent.

Linux® is the registered trademark of Linus Torvalds in the U.S. and other countries.
