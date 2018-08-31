![alt ngrx](http://m0ru.github.io/rx-presentation/images/rx_logo.png)
# @ngrx
Reactive libraries for Angular

[Github](https://github.com/ngrx/platform)

## Packages

- [@ngrx/store](./store/README.md) - RxJS powered state management for Angular applications, inspired by Redux
- [@ngrx/effects](./effects/README.md) - Side Effect model for @ngrx/store to model event sources as actions.
- [@ngrx/router-store](./router-store/README.md) - Bindings to connect the Angular Router to @ngrx/store
- [@ngrx/store-devtools](./store-devtools/README.md) - Store instrumentation that enables a
  [powerful time-travelling debugger](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=en).
- [@ngrx/entity](./entity/README.md) - Entity State adapter for managing record collections.
- [@ngrx/schematics](./schematics/README.md) - Scaffolding library for Angular applications using NgRx.

## How to generate with Nx angular CLI

```
ng g @ngrx/schematics:store State --project=<projectname> --module app.module
```

List of component for ngrx:
> @ngrx/schematics:store
> @ngrx/schematics:entity
> @ngrx/schematics:effects
> @ngrx/schematics:feature
