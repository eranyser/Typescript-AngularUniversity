On-going Seed
===================
On-going seed project.

# Release 01
This first seed includes:

 1. Webpack - the simplest way to use webpack.
 2. typescript loader
 3. css & scss loaders

Loaders are those things that transfer our code from one thing to another.

# Useful Links

> those are useful links:

What is webpack
  - [Webpack 2 Official Site](https://webpack.js.org/)

Installation & Getting Started
  - [Getting Started Guide](https://webpack.js.org/guides/getting-started/)

Webpack Loaders
  - [CSS Loader](https://webpack.js.org/guides/asset-management/)
  - [Sass/SCSS Loader](https://webpack.js.org/loaders/sass-loader/)

I've just created a release branch. In addition I want to create a release.
You can find what is a release [here](https://help.github.com/articles/creating-releases/)

Release 02
==========
In this release I want to copy the ***index.html*** file from the *src* directory to the *dist* directory
For this reason we use: [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin)

A good explanation Video by Mirko Nasato of how to use this loader can be found [here](https://www.youtube.com/watch?v=lPhZW8ZyUA4&list=PLgGUMhSgtxJyIQ4vI3BzlCzZLHL79Ew6p&index=5) and also in Stack-Overflow [here](https://stackoverflow.com/questions/32155154/webpack-config-how-to-just-copy-the-index-html-to-the-dist-folder/34925111)

Release 03
=========
In this release I am upgrading the current code:

 1. Importing a *Person* Object in index.ts from module.ts file to see that typescript is working.
 2. adding a watch script in webpack.config.js
 3. adding resolve extentions in webpack.config.js

Release 04
==========

 1. adding the files in folder  ./dist to .gitignore.
 2. Creating one css bundle for all our css/scss files.
	 1. we are using *extract-text-webpack-plugin*
	 2. replacing the rules in webpack.config.js
The plugin creates the file in the output directory, in our case ./dist. and insert the *link* tag to the index.html file.

Release 05
==========

 1. Add source map to both javascript & css files.
 2. adding *devtool: 'inline-source-map'* to our webpack.config.js
 3. adding source maps to css by changing the *extract-text-webpack-plugin*

Release 06
==========
**Create multiple bundles**

 1. Change the entry point in the webpack.config.js to include several enty points
 2. change the output to inlcude the [name] prefix.
 3. Adding clean-webpack-plugin to clean the dist folder each time we do the build.
 4. Adding webpack-dev-server, in the webpack.config.js tell the server where to take the files. and add
    a new script to package.json.

Release 06
==========
 1. Adding *core-js* to package.json.
	 core-js provide es6 support for those browsers that don't yet support all new es6 features. Although typescript converts all our es6 code to es5 code, es6 introduced not only new syntax features but also new objects and methods to this standard library. things like arrow function or 'back-ticks' string are syntax features, and the typescript compiler converts them to es5 code. but things like Promises or new methods like String.repeat, they are not about syntax they are part of the standard library. in es6 Promise is available as a Global object. so *core-js* provide all those objects and methods for browsers that don't have them already.
libraries like *core-js* that support new standard for old browsers are usually called *polifills* or *shims* *core-js* is not the only option, we can use es6-shim instead, but is seems that core-js works better especially in IE.
 2. Although we installed *core-js* as explained in section 1, it is not enough. After compilation we still gets error that the compiler can't find name such as *Promies, Map, Set* etc. Those are global objects that were added in the es6 specifications. Why is that typescript doesn't know about this *Promise* object? One reason is cause we set the target to be es5, (in tsconfig.json), we generate code for browsers supported es5 and they don't have the global promise or other es6 objects and methods.  However we have the *core-js* as a dependency and this library provides all those objects and methods includein *Promise* so we need a way to tell typescript that we have a library that contains all those objects. We can't point typescript to core-js itself cause core js is written in plain javascript. so it doesn't decalare any type or interfaces or any sort of information required by typescript. the solution is to provide a *declaration files*. this allow us to take an existing javasctipt library and declare each object and method in that library so it can be used with typescript. thankfully we don't need to write such a definition file by ourselves, there are type definition for most popular javascript libraries. As for Typescript 2.0 there is the @types npm organization for obtaining type definitions with npm.
 you can read about it [here](https://blogs.msdn.microsoft.com/typescript/2016/06/15/the-future-of-declaration-files/) and also [here](https://stackoverflow.com/questions/37548066/typescript-typings-in-npm-types-org-packages)
 For now, we must add @types/core-js to our package.json.
 3. adding import "core-js"; to index.js to load this library. this library includes all global objects and there is no explicit load for each one of the globals.

Release 07
==========

 1. Script to build a production version

 Release 08
 ==========

  1. update tsconfig.json to support:
        1. way of importing modules.
        2. adding lib entries to recognize Promise etc.