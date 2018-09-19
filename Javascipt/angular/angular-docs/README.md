# Angular core note

Author: Long Le

Email: levanlong.91@gmail.com


## Modules

### NgModule metadata

- *declarations*: The components, directives, and pipes that belong to this NgModule.
- *exports*: The subset of declarations that should be visible and usable in the component templates of other NgModules.
- *imports*: Other modules whose exported classes are needed by component templates declared in this NgModule.
- *providers*: Creators of services that this NgModule contributes to the global collection of services; they become accessible in all parts of the app. (You can also specify providers at the component level, which is often preferred.)
- *bootstrap*: The main application view, called the root component, which hosts all other app views. Only the root NgModule should set the bootstrap property.


## Component

### Component metadata

- *selector*: A CSS selector that tells Angular to create and insert an instance of this component wherever it finds the corresponding tag in template HTML. For example, if an app's HTML contains <app-hero-list></app-hero-list>, then Angular inserts an instance of the HeroListComponent view between those tags.

- *templateUrl*: The module-relative address of this component's HTML template. Alternatively, you can provide the HTML template inline, as the value of the template property. This template defines the component's host view.

- *providers*: An array of providers for services that the component requires. In the example, this tells Angular how to provide the HeroService instance that the component's constructor uses to get the list of heroes to display.

### Lifecycle Hooks

A component has a lifecycle managed by Angular.

Angular creates it, renders it, creates and renders its children, checks it when its data-bound properties change, and destroys it before removing it from the DOM.

Hook  |	Purpose and Timing
---   | ---
```ngOnChanges()``` | Respond when Angular (re)sets data-bound input properties. The method receives a SimpleChanges object of current and previous property values. Called before ngOnInit() and whenever one or more data-bound input properties change.

```ngOnInit()``` | Initialize the directive/component after Angular first displays the data-bound properties and sets the directive/component's input properties. Called once, after the first ngOnChanges().

```ngDoCheck()``` | Detect and act upon changes that Angular can't or won't detect on its own. Called during every change detection run, immediately after ngOnChanges() and ngOnInit().

```ngAfterContentInit()``` | Respond after Angular projects external content into the component's view / the view that a directive is in. Called once after the first ngDoCheck().

```ngAfterContentChecked()``` | Respond after Angular checks the content projected into the directive/component. Called after the ngAfterContentInit() and every subsequent ngDoCheck().

```ngAfterViewInit()```	| Respond after Angular initializes the component's views and child views / the view that a directive is in. Called once after the first ngAfterContentChecked().

```ngAfterViewChecked()``` | Respond after Angular checks the component's views and child views / the view that a directive is in. Called after the ngAfterViewInit and every subsequent ngAfterContentChecked().

```ngOnDestroy()```	| Cleanup just before Angular destroys the directive/component. Unsubscribe Observables and detach event handlers to avoid memory leaks. Called just before Angular destroys the directive/component.

## Services and dependency injection

### Services
- Service is a broad category encompassing any value, function, or feature that an app needs.

- Angular distinguishes components from services to increase modularity and reusability.

- A component can delegate certain tasks to services, such as fetching data from the server, validating user input, or logging directly to the console.

- Services can depend on other services.

### Dependency injection (DI)

- DI is wired into the Angular framework and used everywhere to provide new components with the services or other things they need. Components consume services; that is, you can inject a service into a component, giving the component access to that service class.

- To define a class as a service in Angular, use the ```@Injectable()``` decorator to provide the metadata that allows Angular to inject it into a component as a dependency.

- When Angular creates a new instance of a component class, it determines which services or other dependencies that component needs by looking at the constructor parameter types.