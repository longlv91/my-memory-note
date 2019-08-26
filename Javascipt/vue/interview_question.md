# <h1 align="center">Vue Interview Question</h1>

Ref: [FullStack Cafe](https://www.fullstack.cafe/)


## What is Vue.js?

Way 1: Vue js is progressive javascript script used to create dynamic user interfaces.Vue js is very easy to learn.In order to work with Vue js you just need to add few dynamic features to a website.You don’t need to install any thing to use Vue js just need add Vue js library in your project.

Way 2: The Vue.js is a progressive JavaScript framework and used to building the interactive user interfaces and also it’s focused on the view layer only (front end). The Vue.js was developed by “Evan You”, an Ex Google software engineer. The latest version is Vue.js 2. The Vue.js 2 is very similar to Angular because Evan You was inspired by Angular.

## How to create an instance of Vue.js?

Every Vue application starts by creating a new Vue instance with the Vue function:
```
var vm = new Vue({
  // options
})
```

## List some features of Vue.js

Vue js comes with following features

- Templates
- Reactivity
- Components
- Transitions
- Routing

## Explain the differences between one-way data flow and two-way data binding?

In one-way data flow the view(UI) part of application does not updates automatically when data Model is change we need to write some custom code to make it updated every time a data model is changed. In Vue js v-bind is used for one-way data flow or binding.

In two-way data binding the view(UI) part of application automatically updates when data Model is changed. In Vue.js v-model directive is used for two way data binding.

## How to create Two-Way Bindings in Vue.js?

v-model directive is used to create Two-Way Bindings in Vue js.In Two-Way Bindings data or model is bind with DOM and Dom is binded back to model.

In below example you can see how Two-Way Bindings is implemented.
```
<div id="app">
  {{message}}
  <input v-model="message">
</div>
<script type="text/javascript">
  var message = 'Vue.js is rad';
  new Vue({ el: '#app', data: { message } });
</script>
```

## What are filters in Vue.js?

In Vue js filters are used to transform the output that are going to rendered on browser.

A Vue.js filter is essentially a function that takes a value, processes it, and then returns the processed value. In the markup it is denoted by a single pipe (|) and can be followed by one or more arguments:
```
<element directive="expression | filterId \[args...\]"></element>
```

## What are Components in Vue.js?

Components are one of most powerful features of Vue js.In Vue components are custom elements that help extend basic HTML elements to encapsulate reusable code.

Following is the way to register a Vue component inside another component:
```
export default {
  el: '#your-element'
  components: {
      'your-component'
  }
}
```

## What are Directives in Vue.js, List some of them you used?

The concept of directive in Vue js is drastically simpler than that in Angular. Vue.js directives provides a way to extend HTML with new attributes and tags. Vue.js has a set of built-in directives which offers extended functionality to your applications.You can also write your custom directives in Vue.js .

Below are list of commonly used directives in Vue.js
- v-show
- v-if
- v-model
- v-else
- v-on

## How can you redirect to another page in Vue.js?

If you are using vue-router, you should use router.go(path) to navigate to any particular route. The router can be accessed from within a component using this.$router. router.go() changed in VueJS 2.0. You can use router.push({ name: "yourroutename"})or just router.push("yourroutename") now to redirect.

## Can I pass parameters in computer properties in Vue.js?

You can use a method or computed function.

The method way:
```
<span>{{ fullName('Hi') }}</span>

methods: {
  fullName(salut) {
      return `${salut} ${this.firstName} ${this.lastName}`
  }
}
```
Computed property with a parameter way:
```
computed: { 
    fullName() {
        return salut => `${salut} ${this.firstName}         
         ${this.lastName}`
    }
}
```

## How can I fetch query parameters in Vue.js?

You have access to a $route object from your components, that expose what we need.
```
//from your component
console.log(this.$route.query.test)
```

## How to use local storage with Vue.js?

You can just do following:
```
localStorage.setItem('YourItem', response.data)
localStorage.getItem('YourItem')
localStorage.removeItem('YourItem')
```

## What are the Advantages/Disadvantages of Vuejs?

### Vue.js Advantages

- Easy for applications and interfaces development
- Support Two-way communication as like AngularJs
- Ability to control the states
- Natural thought process
### Vue.js Disadvantages

- Limited scope
- Single creator
- Small developer community

## Explain the basic logical Vue.js app organisation

A Vue.js application consists of a root Vue instance created with new Vue, optionally organized into a tree of nested, reusable components. For example, a todo app’s component tree might look like this:
```
Root Instance
└─ TodoList
   ├─ TodoItem
   │  ├─ DeleteTodoButton
   │  └─ EditTodoButton
   └─ TodoListFooter
      ├─ ClearTodosButton
      └─ TodoListStatistics
```
All Vue components are also Vue instances.

## What is filters in Vue.js?

## 