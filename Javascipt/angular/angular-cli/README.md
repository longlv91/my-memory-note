## Prerequisites

Both the CLI and generated project have dependencies that require Node 6.9.0 or higher, together
with NPM 3 or higher.

## Installation

**BEFORE YOU INSTALL:** please read the [prerequisites](#prerequisites)
```bash
npm install -g @angular/cli
```

## Usage

```bash
ng help
```

### Generating and serving an Angular project via a development server

```bash
ng new PROJECT-NAME
cd PROJECT-NAME
ng serve
```
You can configure the default HTTP host and port used by the development server with two command-line options :

```bash
ng serve --host 0.0.0.0 --port 4201
```
### Generating Components, Directives, Pipes and Services

You can use the `ng generate` (or just `ng g`) command to generate Angular components:

```bash
ng generate component my-new-component
ng g component my-new-component # using the alias

# components support relative path generation
# if in the directory src/app/feature/ and you run
ng g component new-cmp
# your component will be generated in src/app/feature/new-cmp
# but if you were to run
ng g component ./newer-cmp
# your component will be generated in src/app/newer-cmp
# if in the directory src/app you can also run
ng g component feature/new-cmp
# and your component will be generated in src/app/feature/new-cmp
```
You can find all possible blueprints in the table below:

Scaffold  | Usage
---       | ---
[Component](https://github.com/angular/angular-cli/wiki/generate-component) | `ng g component my-new-component`
[Directive](https://github.com/angular/angular-cli/wiki/generate-directive) | `ng g directive my-new-directive`
[Pipe](https://github.com/angular/angular-cli/wiki/generate-pipe)           | `ng g pipe my-new-pipe`
[Service](https://github.com/angular/angular-cli/wiki/generate-service)     | `ng g service my-new-service`
[Class](https://github.com/angular/angular-cli/wiki/generate-class)         | `ng g class my-new-class`
[Guard](https://github.com/angular/angular-cli/wiki/generate-guard)         | `ng g guard my-new-guard`
[Interface](https://github.com/angular/angular-cli/wiki/generate-interface) | `ng g interface my-new-interface`
[Enum](https://github.com/angular/angular-cli/wiki/generate-enum)           | `ng g enum my-new-enum`
[Module](https://github.com/angular/angular-cli/wiki/generate-module)       | `ng g module my-module`

## Behind sence
### What does the compiler do?

Now that you know what Angular does we can talk about what the compiler does. I will avoid getting too technical mainly because I'm ignorant. However, in a dependency injection system you typically have to express your dependencies with some kind of metadata (e.g. how does a class say I can be injected, My lifetime is blah, or You can think of me as a Component type of instance). In Java, Spring originally did this with XML files. Java later adopted annotations and they have become the preferred way to express metadata. C# uses attributes to express metadata.

Javascript does not have a great mechanism for exposing this metadata builtin. angular-js made an attempt and it wasn't bad but there were a lot of rules that couldn't be easily checked and were a little confusing. With Angular there are two supported ways of specifying the metadata. You can write pure Javascript and specify the metadata manually, somewhat similar to angular-js and just keep following the rules and writing extra boiler-platey code. Alternatively, you can switch to TypeScript which, as it just so happens, has decorators (those @ symbols) which are used to express metadata.

So here is where we can finally get to the compiler. The compiler's job is to take that metadata and create the system of working pieces that is your application. You focus on all the pieces and all of the metadata and the compiler builds one big interconnected application.

### How does the compiler do it?

There are two ways the compiler can work, runtime and ahead-of-time. From here on I will assume you are using TypeScript:

- *Runtime*: When the typescript compiler runs it takes all the decorator information and shoves it into the Javascript code attached to the decorated classes, methods, and fields. In your index.html you reference your main.js which calls the bootstrap method. That method is passed your top level module.
The bootstrap method fires up the runtime compiler and gives it a reference to that top level module. The runtime compiler then starts to crawl that module, all services, components, etc. referenced by that module, and all of associated metadata, and builds up your application.

- *AOT*: Rather than do all the work at runtime Angular has provided a mechanism for doing most the work at build time. This is almost always done using a webpack plugin (this must be one of the most popular yet least known npm packages). It runs after the typescript compilation has run so it sees essentially the same input as the runtime compiler. The AOT compiler builds up your application just like the runtime compiler but then saves it back out into Javascript.
The advantage here is not just that you can save the CPU time required for the compilation itself, but it also allows you to reduce the size of your application.

### Process build
Angular CLI calls Webpack (Angular CLI's real service is configuring webpack. When you run ng build it isn't much more than a proxy to starting Webpack). Webpack first calls the Typescript compiler, then the angular compiler (assuming AOT), all while bundling your code at the same time.

> Angular CLI => Webpack => TypeScript Compiler => TypeScript Compiler calls the Angular compiler in compile time.