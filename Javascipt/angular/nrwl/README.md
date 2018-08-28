![alt nx](https://nrwl.io/assets/nx-logo.png)
# Nrwl Extensions for Angular
An open source toolkit for enterprise Angular applications. [Reference here](https://nrwl.io/nx)

## What is Nx?
Nx is an extension for the the Angular CLI implementing the monorepo-style development. It is also a collection of runtime libraries, linters, and code generators helping large teams build better with Angular.

## Installing Nx
An Nx workspace is an Angular CLI project that has been enhanced to be enterprise ready. Being an Angular CLI project means it will be handy to have the Angular CLI installed globally, which can be done via npm or yarn as well.
```
npm install -g @angular/cli @nrwl/schematics
```

### Creating a New Nx Workspace
```
create-nx-workspace myworkspacename
```

What you end up with is a Nx Workspace with the following files/folders created.
```
apps/
libs/
tools/
angular.json
nx.json
tslint.json
tsconfig.json
```

It's similar to the standard Angular CLI projects with a few changes:

- It has an apps dir where all applications are placed
- It has a libs dir where all custom library code is placed

### Creating an App

Adding new apps to an Nx Workspace is done by using the Angular CLI generate command. Nx has a schematic named app that can be used to add a new app to our workspace:
```
ng generate app myapp
ng generate application myapp # same thing
```

This will create a new app, will place it in the apps directory, and will configure the *angular.json* and *nx.json* files to support the new app. It will also configure the root NgModule to import the NxModule code so we can take advantage of things like *DataPersistence*.

Run `ng generate app --help` to see the list of available options

Most of these options are identical to the ones supported by the default CLI application, but the following are new or different: directory, routing, and tags.

- `ng generate app myapp --directory=myteam` will create a new application in apps/myteam/myapp.
- `ng generate app myapp --routing` will configure the root NgModule to wire up routing, as well as add a <router-outlet> to the AppComponent template to help get us started.
- `ng generate app myapp --tags=shared`,experimental will annotate the created app with the two tags, which can be used for advanced code analysis. Read more below.

### Creating a Lib

Adding new libs to an Nx Workspace is done by using the Angular CLI generate command, just like adding a new app.
```
ng generate lib mylib
ng generate library mylib # same thing
```
Most of these options are identical to the ones supported by the default CLI library, but the following are new or different: directory, routing, lazy, parent-module, publishable, and tags.

- `ng generate lib mylib --directory=myteam` will create a new application in libs/myteam/mylib.
- `ng generate lib mylib --routing` will configure the lib's NgModule to wire up routing to be loaded eagerly.
- `ng generate lib mylib --routing --lazy` will configure the lib's NgModule to wire up routing to be loaded lazily.
- `ng generate lib mylib --routing --parent-module=apps/myapp/src/app/app.module.ts` will configure the lib's NgModule to wire up routing and will configure app.module.ts to load the library.
- `ng generate lib mylib --routing --lazy --parent-module=apps/myapp/src/app/app.module.ts` will configure the lib's NgModule to wire up routing and will configure app.module.ts to load the library.
- `ng generate lib mylib --publishable` will generate a few extra files configuring for ng-packagr. You can then run ng build mylib to create an npm package you can publish to a npm registry. This is very rarely needed when developing in a monorepo. In this case the clients of the library are in the same repository, so no packaging and publishing step is required.
- `ng generate lib mylib --tags=shared`,experimental will annotate the created lib with the two tags, which can be used for advanced code analysis. Read more below.

## Source code demo

[Bitbucket Repository](https://bitbucket.org/longlv91/nx-angular6/)